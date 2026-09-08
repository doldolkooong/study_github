---
type: source
source_url: "https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY12-26.08.24"
source_title: "[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY12 (26.08.24)"
source_id: 7e850b90-06d1-4905-a005-9b558ce1ad56
source_author: doldolkoong
source_published: 2026-08-26
source_updated: 2026-09-05
archived: 2026-09-08
tags:
  - velog-source
---

# [플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY12 (26.08.24)

[Velog 원문](https://velog.io/@doldolkoong/%ED%94%8C%EB%A0%88%EC%9D%B4%EB%8D%B0%EC%9D%B4%ED%84%B0-SK%EB%84%A4%ED%8A%B8%EC%9B%8D%EC%8A%A4-Family-AI-%EC%BA%A0%ED%94%84-36%EA%B8%B0-DAY12-26.08.24) · [[DAY12 - GitHub 팀 협업과 PR|DAY12 - GitHub 팀 협업과 PR]]

> [!info] 원문 보관
> 2026-09-08 수집한 공개 본문이다. 원문의 설명·코드·표기 오류도 보존했으며 학습 노트의 보완란과 함께 읽는다. 이미지는 원문 외부 링크를 유지하여 인터넷 연결이 필요하다.

---

[플레이데이터 SK네트웍스 Family AI 캠프 36기] DAY12 26.08.24

# Github 브랜치 팀장

팀 프로젝트를 진행할 때 팀장은 레파지토리를 만들고, 브랜치 보호 규칙을 설정하고, 팀원을 초대해서 Pull Request(PR) 기반으로 협업이 굴러가게끔 세팅해야 한다. 오늘은 팀장 입장에서 처음부터 끝까지 이 흐름을 직접 세팅해봤다.

<br>

## 1. 레파지토리 생성

GitHub에서 새 레파지토리를 만든다. `Repository name`에 프로젝트 이름을 적고 `Create repository` 버튼을 누르면 된다. 이때 Public/Private 여부, README 초기화 여부 등도 함께 정할 수 있는데, 팀 프로젝트라면 보통 Private으로 생성하고 팀원들을 나중에 Collaborator로 초대하는 방식을 많이 쓴다.

![](https://velog.velcdn.com/images/doldolkoong/post/aefb62d3-5e67-4139-b73e-0efb378ffdf6/image.png)

<br>

## 2. 브랜치 보호 규칙(Branch Protection Rule) 만들기 (예시는 main 브랜치)

레파지토리를 만들었다고 끝이 아니다. 여러 명이 동시에 작업하다 보면 실수로 `main` 브랜치에 검증되지 않은 코드가 바로 올라갈 수 있는데, 이를 막기 위해 **브랜치 보호 규칙**을 설정한다.

`Settings` → `Branches` → `Add branch protection rule` (구버전 UI 기준 `Add classic branch protection rule`) 순서로 들어간다.

![](https://velog.velcdn.com/images/doldolkoong/post/b73c9e15-0918-44b3-93c4-64e9771f1cba/image.png)

## 3. 브랜치 속성 정하기

여기서 핵심은 **"PR 없이는 아무도 이 브랜치에 직접 push 할 수 없게 만드는 것"**이다.

- `Require a pull request before merging` 체크 → 반드시 PR을 통해서만 병합이 가능하도록 강제한다.
- `Require approvals` 체크 후 승인 인원 수 설정
  - 팀장 1명 + 팀원 1명 구성이면 최소 승인 인원을 **1**로 설정
  - 팀장 1명 + 팀원 2명 이상 구성이면 **2** 이상으로 설정해서 최소한의 코드 리뷰 절차를 거치도록 한다.
- `Do not allow bypassing the above settings` 체크 → 관리자(팀장)라도 이 규칙을 우회해서 강제로 push 하지 못하게 막는다. 이걸 켜야 규칙이 말 그대로 "예외 없이" 적용된다.

설정을 마쳤으면 저장한다.

## 4. branch protection rules가 잘 만들어졌는지 확인

설정 후 `Branches` 메뉴로 돌아가면 방금 만든 규칙이 목록에 나타난다. 규칙 이름, 대상 브랜치, 적용된 옵션(승인 필요 인원 등)이 제대로 반영됐는지 한 번 더 확인하는 습관을 들이면 좋다.

![](https://velog.velcdn.com/images/doldolkoong/post/ba67ccce-ccc4-4026-a9e5-77480b7458f6/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/ec59f15b-be12-4a74-891d-b09b90891e79/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/5597a958-0b8a-46e5-a08d-bc47489fc2fa/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/2d6e93d3-c0e1-43e6-a2df-815ba613375b/image.png)

## 5. GitHub - VSCode 연결하기

이제 로컬 개발 환경(VSCode)에서 이 레파지토리를 클론해서 작업할 수 있도록 연결한다.

1. GitHub 레파지토리 페이지에서 `Code` 버튼 → `HTTPS` 탭 → 표시된 URL을 복사한다.

   ![](https://velog.velcdn.com/images/doldolkoong/post/1c18642c-c3e0-44ce-b3be-638fba5f9afb/image.png)

2. VSCode에서 `Ctrl+Shift+P`로 명령 팔레트를 연 뒤 `Git: Clone`을 입력하고 실행한다. 방금 복사한 URL을 붙여넣고 엔터를 누르면, 저장할 로컬 폴더를 선택하는 창이 뜨고 클론이 진행된다.

   ![](https://velog.velcdn.com/images/doldolkoong/post/6cb06bbd-df0b-443d-a600-57ca78d47567/image.png)

## 6. dev 브랜치 만들기

실무에서는 `main` 브랜치에 바로 작업하지 않고, 개발용 브랜치(보통 `dev`)를 따로 두고 그 위에서 작업한 뒤 검증이 끝나면 `main`으로 병합하는 방식을 많이 쓴다. 이를 위해 `dev` 브랜치를 새로 만든다.

- VSCode 좌측 하단의 브랜치 이름(`main`)을 클릭하면 브랜치 선택/생성 메뉴가 뜬다.
- `Create new branch from...` → 기준 브랜치로 `main` 선택 → 브랜치 이름을 `dev`로 입력하면 로컬에 `dev` 브랜치가 생성된다.
- 로컬에서 만든 브랜치는 아직 원격 저장소(GitHub)에는 없는 상태이므로, 좌측 하단 `dev` 옆에 있는 클라우드(↑) 아이콘을 눌러 **Publish Branch**를 해줘야 GitHub에도 `dev` 브랜치가 반영된다.

![](https://velog.velcdn.com/images/doldolkoong/post/71b1b049-dba2-42ce-80d7-5c85305e6ac2/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/c2205abd-2194-4ced-aeec-af3218881404/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/86c9d24b-ba67-4f10-a723-1d0c0da5a5c0/image.png)

## 7. 브랜치가 잘 만들어졌는지 확인하기

GitHub 레파지토리 페이지로 가서 브랜치 목록(기본으로는 `main` 표시 옆 드롭다운, 혹은 상단 브랜치 개수 표시)을 확인하면 방금 Publish한 `dev` 브랜치가 원격에도 생성된 것을 확인할 수 있다.

![](https://velog.velcdn.com/images/doldolkoong/post/c25f6485-5c0c-434a-a2fa-5ed16f21b1fd/image.png)

## 8. 기본 브랜치(Default branch) 변경

팀원들이 새로 클론하거나 PR을 만들 때 기준이 되는 브랜치를 `main`이 아니라 `dev`로 바꿔주면, 이후 작업들이 자연스럽게 `dev` 브랜치를 기준으로 진행된다.

`Settings` → `Default branch` 항목에서 연필(✏️) 아이콘을 눌러 `dev`로 변경 → `Update` 버튼 클릭 → 확인 메시지에서 `I understand, update the default branch.`를 선택하면 적용된다.

![](https://velog.velcdn.com/images/doldolkoong/post/ad87b149-8efc-4a20-a7d1-4b2f26099b2f/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/517ef003-6215-4dae-a111-84059bc30978/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/f0c93416-3510-44b9-9ae3-b44b74770edf/image.png)

기본 브랜치가 `dev`로 변경된 것을 확인할 수 있다.

![](https://velog.velcdn.com/images/doldolkoong/post/67125c52-c12e-4e5f-bc50-d1f86313d0b6/image.png)

## 9. 팀원 초대하기

Private 레파지토리는 초대받은 사람만 접근할 수 있기 때문에, 팀원들을 Collaborator로 등록해줘야 한다.

`Settings` → `Collaborators` → `Manage access` → `Add people` 클릭 → 팀원의 GitHub 닉네임이나 가입한 이메일을 입력해서 검색 → 목록에서 선택 후 `Add [이름] to this repository`를 누르면 초대가 발송된다. 초대받은 팀원은 이메일이나 GitHub 알림을 통해 초대를 수락해야 실제로 레파지토리에 접근할 수 있다.

![](https://velog.velcdn.com/images/doldolkoong/post/dfa44209-ab89-4f80-8764-a0543e2f0a7a/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/f02840b8-33ff-45b5-a22b-fd176e8e0475/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/ee162da9-e455-4790-abe7-2caf31914135/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/5f5f9ad5-5d90-41d6-8529-afc1098f452f/image.png)

## 10. 팀원이 만든 파일 커밋하기(PR 확인)

팀원이 자신의 브랜치에서 작업한 내용을 push하고 PR을 생성하면, 레파지토리의 `Pull requests` 탭에 숫자 뱃지가 뜬다. 이 숫자는 "현재 검토 대기 중인 PR이 있다"는 뜻이지, 단순히 팀원이 pull을 받았다는 의미가 아니라 **팀원이 작업물을 올리고 병합을 요청했다**는 뜻으로 이해하면 된다.

![](https://velog.velcdn.com/images/doldolkoong/post/165e2013-170c-4bc4-9aa9-bfe484ea9fbe/image.png)

## 11. 팀원들이 올린 PR 확인 및 병합

`Pull requests` 탭에서 팀원이 올린 PR을 클릭하면, 변경된 파일 목록과 구체적인 코드 변경 사항(diff)을 확인할 수 있다.

![](https://velog.velcdn.com/images/doldolkoong/post/19e01b17-a598-44b8-a7c8-a99aa0c796b3/image.png)

내용을 검토했을 때 문제가 없다면, `Add a comment`에 리뷰 코멘트(예: 확인했다는 메모, 수정 제안 등)를 남기고 `Comment`를 눌러 리뷰 기록을 남긴다.

![](https://velog.velcdn.com/images/doldolkoong/post/abe7be8b-c12f-4c3a-9b59-b010b0288d43/image.png)

![](https://velog.velcdn.com/images/doldolkoong/post/d4f454ae-0f97-4c68-a466-bb463c5f3991/image.png)

리뷰까지 마치고 이상이 없다면 `Merge pull request`를 눌러 실제 병합을 진행한다.

![](https://velog.velcdn.com/images/doldolkoong/post/66e1ec99-2346-47a7-8974-111c0dbbd496/image.png)

`Confirm merge`를 누르면 팀원의 브랜치(예: `dev`로 올린 작업)가 기준 브랜치인 `main`으로 병합된다.

![](https://velog.velcdn.com/images/doldolkoong/post/681673cc-f464-40eb-996a-1f7a2330e059/image.png)

병합이 정상적으로 완료된 것을 PR 화면에서 확인할 수 있다.

![](https://velog.velcdn.com/images/doldolkoong/post/e1781ee8-3964-43e2-85a5-77902d85bdb6/image.png)

실제로 `main` 브랜치로 이동해서 파일을 확인해보면, 팀원이 작업한 내용이 반영되어 병합이 잘 된 것을 확인할 수 있다.

![](https://velog.velcdn.com/images/doldolkoong/post/120f7b50-7802-4e5a-832c-072f7adb01c9/image.png)

<br>


