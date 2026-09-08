# Obsidian 공부 시스템 — 최종 깔끔 버전

AI 자동요약 자동화는 제거했습니다.

남기는 기능은 딱 4개입니다.

1. QuickAdd로 공부 노트 자동 생성
2. WikiDocs 스타일 공부 노트
3. 1일 / 7일 / 30일 복습 자동 분류
4. Review Dashboard

AI 요약은 ChatGPT에 노트를 붙여넣어 수동으로 진행합니다.

---

## Vault 구조

```text
playdata/
├─ 00_Dashboard/
│  ├─ Study Dashboard.md
│  ├─ Review Dashboard.md
│  └─ AI 요약 프롬프트.md
│
├─ 98_Review/
│  ├─ 1D/
│  ├─ 7D/
│  └─ 30D/
│
├─ 99_Templates/
│  ├─ WikiDocs Study Note.md
│  └─ Review Log.md
│
├─ Coding Test/
├─ Deep Learning/
├─ Machin Learning/
└─ python/
```

---

## 필요한 플러그인

- QuickAdd
- Dataview

Templater / Copilot / Shell commands / Codex는 이 시스템에 필요 없습니다.

---

## QuickAdd — 공부 노트

`wikiDocs study note` → ⚙

Template Path:

```text
99_Templates/WikiDocs Study Note.md
```

File Name Format:

```text
{{VALUE:python,Coding Test,Machin Learning,Deep Learning|name:subject|text:🐍 Python,🧩 Coding Test,🤖 Machine Learning,🧠 Deep Learning|label:과목 선택}}/{{VALUE:noteName|label:수업/공부 주제}}
```

추천 단축키:

```text
Ctrl + Alt + N
```

---

## QuickAdd — Review Log

`review log` → ⚙

Template Path:

```text
99_Templates/Review Log.md
```

File Name Format:

```text
98_Review/{{VALUE:1D,7D,30D|name:stage|text:1일 복습,7일 복습,30일 복습|label:복습 단계}}/{{DATE}} - {{VALUE:source|label:원본 노트 제목}} - {{VALUE:stage}}
```

추천 단축키:

```text
Ctrl + Alt + R
```

---

## 실제 사용

### 수업 시작

```text
Ctrl + Alt + N
→ 과목 선택
→ 제목 입력
→ 난이도 선택
→ 노트 작성
```

### 수업 종료

1. 노트 전체 복사
2. `00_Dashboard/AI 요약 프롬프트.md` 열기
3. 프롬프트 + 노트 내용을 ChatGPT에 붙여넣기
4. 결과를 노트의 `🤖 ChatGPT 요약 붙여넣기` 영역에 붙여넣기

### 복습

`00_Dashboard/Review Dashboard.md`

- 오늘 복습
- 밀린 복습
- 1일 예정
- 7일 예정
- 30일 예정

자동 분류.

체크박스를 완료하면 미완료 목록에서 사라집니다.

---

## CSS

설정 → Appearance → CSS snippets에서

```text
wikidocs-study
```

활성화하면 본문 폭 / 제목선 / 표 가독성이 정리됩니다.


---

## QuickAdd — 코딩테스트 노트

새 Choice를 하나 추가합니다.

```text
이름: Coding Test
Type: Template
Template Path: 99_Templates/Coding Test.md
```

File Name Format:

```text
Coding Test/{{VALUE:problemName|label:문제 이름}}
```

추천 단축키:

```text
Ctrl + Alt + C
```

노트 구성은 아래 순서입니다.

```text
<문제>
↓
<코드>
↓
<해설>
↓
1일 / 7일 / 30일 복습
```
