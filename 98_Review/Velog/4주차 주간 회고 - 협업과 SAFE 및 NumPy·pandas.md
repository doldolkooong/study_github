---
type: review
subject: "Machin Learning"
difficulty: "중급"
created: 2026-09-08
review_1d: 2026-09-09
review_7d: 2026-09-15
review_30d: 2026-10-08
status: prepared
stage: "주간 회고 정리"
source: "[[90_Sources/Velog/08 - 4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas - 원문]]"
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-4%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84%ED%9A%8C%EA%B3%A0-26.08.24-26.08.28"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] 4주차 주간회고 (26.08.24 ~ 26.08.28)"
source_published: 2026-08-31
source_updated: 2026-09-03
source_id: 3b1aca7a-b503-409a-9160-699e1a703fe9
source_author: doldolkoong
template: "99_Templates/Review Log.md"
tags:
  - study
  - velog
  - review
---

# 4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas

[원문 보기](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-4%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84%ED%9A%8C%EA%B3%A0-26.08.24-26.08.28) · 2026-09-08 정리

> [!attention] 원문 확인·보완
> 제목은 4주차지만 본문 첫 문장은 2주차로 되어 있다. 2026-08-24~28의 4주차 회고로 정리했다.

> [!info] 복습 준비 자료
> 기존 주간 회고를 Review Log 구조로 정리했다. 아래 답안은 원문 기반 참고 답안이며 사용자가 원본 없이 회상하거나 복습을 완료했다는 기록은 아니다.

## 1. 원본 안 보고 적기

### 핵심 개념 3개

1. 협업: 배운 내용과 경험을 먼저 말해보기.
2. 프로젝트: 배운 내용과 경험을 먼저 말해보기.
3. 분석 기초: 배운 내용과 경험을 먼저 말해보기.

<details>
<summary>원문 기반 참고 답안</summary>

1. **협업**: 브랜치 보호와 PR 검토 절차를 직접 구성했다.
2. **프로젝트**: 요구사항·데이터 정의 → 전처리·DB → 분석·웹 구현으로 이어졌다.
3. **분석 기초**: shape·axis를 익히고 Series·DataFrame·groupby·map·apply를 실습했다.

</details>

### 핵심 코드 / 공식

**회상 문제:** groupby 결과가 Series라면 10·20·30 라벨만 고르는 방법은?

<details>
<summary>해설 보기</summary>

인덱스가 실제로 10·20·30인지 확인한 뒤 `.loc[[10,20,30]]`로 선택한다. 존재하지 않는 라벨 가능성은 reindex로 다룬다.

</details>

## 2. 원본 확인 후 틀린 부분

- 내가 틀리게 기억한 것: 실제 복습 후 기록.
- 정확한 내용: 위 해설 및 연결된 수업 노트와 대조.

### 원문에 기록한 경험과 다음 행동

- 계속할 것: 역할을 나누고 실제 결과를 서비스 화면으로 확인하는 학습.
- 보완할 것: MySQL 재설치 시간과 groupby 결과 선택에서의 어려움.
- 다음 연습: 요구사항을 다시 점검하고 연령대별 집계 문제를 직접 푼다.

## 3. 1분 설명

> 참고 답안: Git 협업부터 SAFE 프로젝트, NumPy·pandas까지 연결하고 환경 복구와 집계 연습을 보완한다. 브랜치 보호와 PR 검토 절차를 직접 구성했다. 요구사항·데이터 정의 → 전처리·DB → 분석·웹 구현으로 이어졌다. shape·axis를 익히고 Series·DataFrame·groupby·map·apply를 실습했다.

## 4. 복습 체크

- [ ] 개념을 말로 설명했다.
- [ ] 코드 또는 처리 흐름을 보지 않고 다시 작성했다.
- [ ] 실수 포인트를 다시 확인했다.
- [ ] 관련 개념과 연결했다.

## 5. 이번 복습 결과

- 이해도: 미평가 — 실제 복습 후 기입.
- 다음에 다시 볼 것: [[DAY12 - GitHub 팀 협업과 PR|DAY12 - GitHub 팀 협업과 PR]], [[SAFE - 요구사항 정의|SAFE - 요구사항 정의]], [[SAFE - 모델 모듈화 및 웹 서비스 구현|SAFE - 모델 모듈화 및 웹 서비스 구현]], [[DAY16 - 기초 통계와 NumPy 배열|DAY16 - 기초 통계와 NumPy 배열]], [[DAY17 - 벡터와 pandas 그룹 분석|DAY17 - 벡터와 pandas 그룹 분석]]

# 🔁 복습 스케줄

- [ ] **1일 복습** [stage:: 1D] [due:: 2026-09-09]
- [ ] **7일 복습** [stage:: 7D] [due:: 2026-09-15]
- [ ] **30일 복습** [stage:: 30D] [due:: 2026-10-08]

### 복습 방법

1. 요약을 가리고 핵심 개념 3개를 설명한다.
2. 예제 또는 처리 흐름을 보지 않고 재현한다.
3. 해설과 비교하고 틀린 부분을 기록한다.
4. 실제 복습을 마친 뒤 체크한다.

## 🔗 관련 노트

- [[DAY12 - GitHub 팀 협업과 PR|DAY12 - GitHub 팀 협업과 PR]]
- [[SAFE - 요구사항 정의|SAFE - 요구사항 정의]]
- [[SAFE - 모델 모듈화 및 웹 서비스 구현|SAFE - 모델 모듈화 및 웹 서비스 구현]]
- [[DAY16 - 기초 통계와 NumPy 배열|DAY16 - 기초 통계와 NumPy 배열]]
- [[DAY17 - 벡터와 pandas 그룹 분석|DAY17 - 벡터와 pandas 그룹 분석]]
- [[00_Dashboard/Velog 학습 자료 목차|전체 32개 글 목차]]

## 📎 원문과 확인 자료

- [Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-4%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84%ED%9A%8C%EA%B3%A0-26.08.24-26.08.28)


> [!quote]- 원문 전체 보기 — 코드·표·이미지 링크 포함
> ![[90_Sources/Velog/08 - 4주차 주간 회고 - 협업과 SAFE 및 NumPy·pandas - 원문]]
