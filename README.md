# expert-panel-by-ebp

근거 기반(Evidence-Based Practice) 전문가 패널 토론 스킬 for [Claude Code](https://claude.com/claude-code).

주어진 주제에 대해 **관련 학문 분야의 근거를 먼저 탐색**한 후, 해당 근거에 기반한 6인 전문가 패널이 토론하고, 사용자 맥락에 맞춘 최소 실험(MVE)까지 설계합니다.

> "전문가가 이렇다고 해서 무조건 따르지 않는다. 근거 없는 전문가 조언은 안 하느니만 못할 수 있다." — EBP 원칙

## 왜 만들었나

LLM에게 "전문가처럼 답해줘"를 시키면 권위 인용에 의존한 그럴듯한 답변이 나오기 쉽습니다. 이 스킬은 그 단계를 분리해 (1) **근거를 먼저 깔고** → (2) 그 위에서 전문가가 토론하게 하고 → (3) **사용자 자신의 맥락에 맞춘 최소 실험**으로 닫습니다.

## 6축 매핑 (Harness Engineering)

| 축 | 어디서 적용되나 |
|----|----------------|
| **구조** | 7단계 layered phase + 단계별 ✓ Gate + 미달 시 fallback |
| **맥락** | 3단계 — `AskUserQuestion`으로 사용자 상황 수집 |
| **계획** | 1-2단계 — 학문 지도 → 근거 지형 (탐색 전 설계) |
| **실행** | 4-6단계 — 근거 태그 강제, Core/Peripheral 분리, MVE 설계 |
| **검증** | ✓ Gate + Hard Rules + Checklist Before Stopping |
| **개선** | 7단계 저장 → PBE(Practice-Based Evidence) 루프로 N-of-1 축적 |

## 설치

폴더 기반 SKILL.md 형식이라 `~/.claude/skills/`에 복사만 하면 끝입니다.

```bash
# 사용자 전역 설치
cp -r skills/expert-panel ~/.claude/skills/

# 또는 프로젝트 로컬 설치
cp -r skills/expert-panel .claude/skills/
```

## 사용법

```
/expert-panel [주제]                          → 전체 7단계 실행
/expert-panel [주제] --quick                  → 1-2단계(근거 탐색) 생략
/expert-panel [주제] --experts [전문가1, ...]  → 전문가 직접 지정
```

트리거 키워드: `전문가소환`, `전문가 패널`, `expert panel`, `근거 기반 분석`, `EBP 분석`.

## 8단계 흐름 (분할 User Gate)

0. **Goal Mirror & 현재 상황** — 텍스트 mirror + `AskUserQuestion` 1개 *(Pre-flight Gate)*
1. **학문 지도** — 주제 관련 학문 분야 2-4개 식별, 주 근거원 선택
2. **근거 지형** — WebSearch로 메타분석/체계적 리뷰 탐색, 5단계 태그 부여
3. **깊은 제약 수집** — 자원·도구·측정기준 `AskUserQuestion` *(Deep Gate)*
4. **패널 토론** — 6인 전문가, 근거 태그 동반 4라운드
5. **구현 설계** — Core/Peripheral Practice 분리, 사용자 맥락 적응
6. **실천 실험** — MVE + 성공/실패 기준 + 반복 주기
7. **저장** — `AskUserQuestion`으로 저장 위치 확인 *(User Gate)*

> **분할 게이트 설계**: harness `specify`/`scaffold`의 "L0 Goal → L1 scan → L2 deep interview" 패턴 차용. 0단계가 1-2단계의 학문/근거 탐색을 사용자 맥락에 좁혀주고, 3단계는 근거를 본 다음에야 의미 있는 답을 얻을 수 있는 자원·제약·측정기준만 수집.

## 근거 수준 체계

| 태그 | 의미 |
|------|------|
| **[Strong]** | 메타분석, 체계적 리뷰, 복수의 재현된 실험 |
| **[Moderate]** | 복수의 RCT 또는 대규모 관찰 연구 |
| **[Emerging]** | 단일 연구, 예비 결과, 파일럿 스터디 |
| **[Expert]** | 전문가 합의, 임상 경험 기반 (근거 약함 — 경고 동반) |
| **[Contested]** | 상반된 연구 결과가 존재 |

학술적 배경: `skills/expert-panel/references/evidence-framework.md` (OCEBM Levels of Evidence 기반).

## 예시

`examples/EBP_타이핑vs말하기속도비교.md` — 실제 산출물.

**같은 입력으로 재현하기**:
```
/expert-panel 타이핑 vs 말하기 속도 비교
```
3단계 `AskUserQuestion`에 다음과 같이 응답:
- 현재 상황: "측정 방법이 통일되지 않은 상태, 본인 기준선 없음"
- 원하는 변화: "동일 단위로 직접 비교 측정"

→ Speech Science + HCI 도메인 식별 → Pellegrino, Ruan, Dhakal, 신지영 등 6인 패널 → "완성 음절/분 통일 + 총 시간 기반 측정" 합의 도출.

## 폴더 구조

```
expert-panel-by-ebp/
├── README.md                          # 이 파일
├── skills/
│   └── expert-panel/
│       ├── SKILL.md                   # 메인 스킬 (v3.1.0)
│       └── references/
│           ├── evidence-framework.md  # OCEBM 기반 근거 수준 학술 배경
│           └── implementation-guide.md # Implementation Science / PBE 심화
├── examples/
│   └── EBP_타이핑vs말하기속도비교.md   # 실제 산출물 예시
└── legacy/
    └── 전문가소환.md                   # v1 flat 파일 (참조용)
```

## v3.1.0 변경점 (vs v3.0.0)

- `allowed-tools` 명시 (Read, WebSearch, Write, AskUserQuestion)
- **분할 User Gate 도입** — 새 0단계(Mirror + 현재 상황) + 기존 3단계(깊은 제약)로 분리
- 0·3·7단계에 `AskUserQuestion` 도구 호출 명시 (이전엔 텍스트로만)
- "Hard Rules" 섹션 추가 (5개 행동 규칙)
- "Checklist Before Stopping" 10항목으로 확장 (0단계 추가)
- 6축 매핑 표 추가 (분할 게이트 반영)
- 폴더 구조로 재배치 (`SKILL.md` + `references/`)

## Credits

- 김창준 — EBP 접근법과 "근거 없는 전문가 조언의 위험성"에 대한 사고의 영감
- team-attention/harness — 6축(구조·맥락·계획·실행·검증·개선) 사이클 프레임워크

## License

MIT
