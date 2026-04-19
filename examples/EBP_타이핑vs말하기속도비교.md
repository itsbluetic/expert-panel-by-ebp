---
tags:
  - ebp
  - 전문가패널
  - speech-science
  - HCI
date: 2026-03-21
---

> 생성일: [[2026-03-21]]

# 타이핑 vs 말하기 속도 — 근거 기반 전문가 패널

## 학문 지도

| 분야 | 관련성 | 핵심 연구 주제 | 근거 풍부도 |
|-----|--------|---------------|-----------|
| Speech Science / Phonetics | 높음 | 말하기 속도(speech rate) 측정, 음절/분 단위 정량화, 언어별 차이 | 풍부 |
| HCI (Human-Computer Interaction) | 높음 | 텍스트 입력 방식 비교(keyboard vs voice), WPM 벤치마크, STT 오류율과 실효 속도 | 풍부 |
| Psycholinguistics | 중간 | 발화 산출(speech production) 속도, 인지 부하와 발화 속도 관계 | 보통 |
| Ergonomics / Productivity Science | 중간 | 입력 방식별 생산성 비교, 피로도, 작업 전환 비용 | 보통 |

**주 근거원**: Speech Science + HCI

## 근거 지형

### 설명적 발견
- **[Strong]** 한국어 일상 발화 속도: ~200-270 음절/분 (정상 성인). 아나운서 ~300, 빠른 대화 350+ — Shin & Kiaer (2015)
- **[Strong]** 교차언어 비교: 음절 수는 다르지만 초당 정보량은 언어 간 거의 동일 — Pellegrino et al. (2011)
- **[Strong]** 평균 타이핑: 전문가 ~80 WPM, 일반인 ~40 WPM (영어) — Dhakal et al. (2018) 136K명
- **[Moderate]** 한국어 500 keystroke/분 → ~170 완성 글자/분 (자모 평균 2.8 keystroke/글자)
- **[Moderate]** STT 실효 속도: raw의 ~60-70% (오류 수정 포함) — Ruan et al. (2018) Stanford

### 처방적 발견
- **[Moderate]** 단순 텍스트 → STT 2-3배 빠름. 구조화된 텍스트 → 타이핑이 효율적
- **[Strong]** articulation rate(순수 발화)과 speech rate(쉼 포함) 구분 필수 — Goldman-Eisler (1968)

### Gottman 경고
- **[Contested]** "말하기가 3-4배 빠르다" — STT 수정 포함 시 실효 1.5-2배
- **[Contested]** "한국어가 영어보다 정보 전달이 빠르다" — 초당 정보량은 동일

## 전문가 패널 (6인)

1. **François Pellegrino** — 비교음성학, 교차언어 발화 속도/정보량 비교
2. **Sherry Ruan** — HCI, 음성 vs 키보드 입력 속도 실증 비교
3. **Vivek Dhakal** — 타이핑 과학, 136K명 대규모 연구
4. **신지영** — 한국어 음성학, 발화 속도/운율/음절 구조
5. **Jonathan Kaye** — 음성인식 엔지니어링, Whisper 모델 정확도
6. **김창준** — 실천 과학, 측정 설계, 실험 루프

## 핵심 합의

- **동일 단위**: 타이핑·말하기 모두 **완성 음절/분**으로 통일
- **총 시간 기반**: 입력 시작~완료까지 wall clock time (생각·수정 포함)
- **실효 속도**: STT 오류 수정 시간 포함 최종 텍스트 기준
- **통제 과제 + 자유 과제** 병행 측정 권장
- 한국어 음절 카운트: 유니코드 완성형 (U+AC00~U+D7A3)

## 나의 기준선

- 타이핑: ~500 keystroke/분 ≈ ~170 음절/분
- 말하기: 측정 필요 (예상 ~250 음절/분 raw, ~200 실효)
- 예상 비율: 1.2~1.5배 (실효 기준)
