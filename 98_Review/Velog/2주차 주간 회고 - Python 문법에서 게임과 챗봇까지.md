---
type: review
subject: "python"
difficulty: "초급"
created: 2026-09-08
review_1d: 2026-09-09
review_7d: 2026-09-15
review_30d: 2026-10-08
status: prepared
stage: "주간 회고 정리"
source: "[[90_Sources/Velog/23 - 2주차 주간 회고 - Python 문법에서 게임과 챗봇까지 - 원문]]"
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-2%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84-%ED%9A%8C%EA%B3%A0"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] 2주차 주간 회고"
source_published: 2026-08-16
source_updated: 2026-09-01
source_id: 6adf1523-068c-45a0-996e-72773afe0c9b
source_author: doldolkoong
template: "99_Templates/Review Log.md"
tags:
  - study
  - velog
  - review
---

# 2주차 주간 회고 - Python 문법에서 게임과 챗봇까지

[원문 보기](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-2%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84-%ED%9A%8C%EA%B3%A0) · 2026-09-08 정리

> [!info] 복습 준비 자료
> 기존 주간 회고를 Review Log 구조로 정리했다. 아래 답안은 원문 기반 참고 답안이며 사용자가 원본 없이 회상하거나 복습을 완료했다는 기록은 아니다.

## 1. 원본 안 보고 적기

### 핵심 개념 3개

1. 제어 흐름: 배운 내용과 경험을 먼저 말해보기.
2. 함수와 객체: 배운 내용과 경험을 먼저 말해보기.
3. 응용: 배운 내용과 경험을 먼저 말해보기.

<details>
<summary>원문 기반 참고 답안</summary>

1. **제어 흐름**: 조건문·반복문·예외처리를 게임에 적용했다.
2. **함수와 객체**: 가변 인자·특수 함수·클래스·Enum을 익혔지만 일부 개념은 추가 복습이 필요했다.
3. **응용**: 표준 라이브러리와 Streamlit을 이용해 게임·챗봇을 만들었다.

</details>

### 핵심 코드 / 공식

**회상 문제:** 숫자 입력을 int로 바꾼 뒤 범위만 검사하면 충분한가?

<details>
<summary>해설 보기</summary>

아니다. 변환 자체가 실패하는 ValueError와 변환 후 범위 오류를 각각 처리해야 한다.

</details>

## 2. 원본 확인 후 틀린 부분

- 내가 틀리게 기억한 것: 실제 복습 후 기록.
- 정확한 내용: 위 해설 및 연결된 수업 노트와 대조.

### 원문에 기록한 경험과 다음 행동

- 계속할 것: 배운 문법을 동작하는 작은 프로그램에 적용한다.
- 보완할 것: 입력 오류·모듈 책임·함수 기본기를 먼저 점검한다.
- 다음 연습: 세 게임의 공통 입력·출력과 개별 규칙을 나눠 구현한다.

## 3. 1분 설명

> 참고 답안: 자료형·함수·클래스를 게임과 챗봇으로 연결하고 입력 검증과 역할 분리를 반복 연습한다. 조건문·반복문·예외처리를 게임에 적용했다. 가변 인자·특수 함수·클래스·Enum을 익혔지만 일부 개념은 추가 복습이 필요했다. 표준 라이브러리와 Streamlit을 이용해 게임·챗봇을 만들었다.

## 4. 복습 체크

- [ ] 개념을 말로 설명했다.
- [ ] 코드 또는 처리 흐름을 보지 않고 다시 작성했다.
- [ ] 실수 포인트를 다시 확인했다.
- [ ] 관련 개념과 연결했다.

## 5. 이번 복습 결과

- 이해도: 미평가 — 실제 복습 후 기입.
- 다음에 다시 볼 것: [[DAY3 - 자료형과 제어문 및 예외 처리|DAY3 - 자료형과 제어문 및 예외 처리]], [[DAY4 - 함수와 특수 함수|DAY4 - 함수와 특수 함수]], [[DAY5 - Enum과 클래스 및 모듈|DAY5 - Enum과 클래스 및 모듈]], [[DAY6 - 표준 라이브러리와 Streamlit|DAY6 - 표준 라이브러리와 Streamlit]], [[DAY7 - 묵찌빠 상태와 챗봇 구조|DAY7 - 묵찌빠 상태와 챗봇 구조]], [[가위바위보·묵찌빠·하나빼기 모듈화|가위바위보·묵찌빠·하나빼기 모듈화]]

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

- [[DAY3 - 자료형과 제어문 및 예외 처리|DAY3 - 자료형과 제어문 및 예외 처리]]
- [[DAY4 - 함수와 특수 함수|DAY4 - 함수와 특수 함수]]
- [[DAY5 - Enum과 클래스 및 모듈|DAY5 - Enum과 클래스 및 모듈]]
- [[DAY6 - 표준 라이브러리와 Streamlit|DAY6 - 표준 라이브러리와 Streamlit]]
- [[DAY7 - 묵찌빠 상태와 챗봇 구조|DAY7 - 묵찌빠 상태와 챗봇 구조]]
- [[가위바위보·묵찌빠·하나빼기 모듈화|가위바위보·묵찌빠·하나빼기 모듈화]]
- [[00_Dashboard/Velog 학습 자료 목차|전체 32개 글 목차]]

## 📎 원문과 확인 자료

- [Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-2%EC%A3%BC%EC%B0%A8-%EC%A3%BC%EA%B0%84-%ED%9A%8C%EA%B3%A0)


> [!quote]- 원문 전체 보기 — 코드·표·이미지 링크 포함
> ![[90_Sources/Velog/23 - 2주차 주간 회고 - Python 문법에서 게임과 챗봇까지 - 원문]]
