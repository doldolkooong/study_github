# 🔁 Review Dashboard

> [!summary] 복습 규칙
> 오늘 날짜가 되면 해당 목록에 나타나고, 체크하면 미완료 목록에서 사라짐.

## 🚨 밀린 복습

```dataview
TASK
FROM #study
WHERE !completed AND due < date(today)
SORT due ASC
```

## 📅 오늘 복습

```dataview
TASK
FROM #study
WHERE !completed AND due = date(today)
SORT file.name ASC
```

## 🌱 1일 복습 예정

```dataview
TASK
FROM #study
WHERE !completed AND stage = "1D" AND due > date(today)
SORT due ASC
```

## 📘 7일 복습 예정

```dataview
TASK
FROM #study
WHERE !completed AND stage = "7D" AND due > date(today)
SORT due ASC
```

## 🧠 30일 복습 예정

```dataview
TASK
FROM #study
WHERE !completed AND stage = "30D" AND due > date(today)
SORT due ASC
```

## ✅ 최근 Review Log

```dataview
TABLE
  stage AS "복습 단계",
  source AS "원본",
  created AS "복습일"
FROM #review
SORT created DESC
LIMIT 20
```
