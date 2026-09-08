# 📚 Study Dashboard

## 🔥 최근 공부 노트

```dataview
TABLE
  subject AS "분야",
  difficulty AS "난이도",
  created AS "작성일",
  file.mtime AS "최근 수정"
FROM #study
SORT file.mtime DESC
LIMIT 15
```

## 🐍 Python

```dataview
LIST
FROM #study
WHERE subject = "python"
SORT file.mtime DESC
LIMIT 10
```

## 🧩 Coding Test

```dataview
LIST
FROM #study
WHERE subject = "Coding Test"
SORT file.mtime DESC
LIMIT 10
```

## 🤖 Machine Learning

```dataview
LIST
FROM #study
WHERE subject = "Machin Learning"
SORT file.mtime DESC
LIMIT 10
```

## 🧠 Deep Learning

```dataview
LIST
FROM #study
WHERE subject = "Deep Learning"
SORT file.mtime DESC
LIMIT 10
```

## 🔁 복습

→ [[Review Dashboard]]
