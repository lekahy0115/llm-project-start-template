# 팀원 공통 협업 절차: Colab 노트북 → GitHub 작업 브랜치 → PR → main

이 문서는 **각 팀원이 반복하여 수행하는 실제 작업 순서**입니다. 관리자용 설정 절차는 포함하지 않습니다. 개발은 `.ipynb` 중심이며, `.py` 파일을 따로 만들 필요가 없습니다.

## 0. 먼저 알아둘 용어

| 용어 | 뜻 |
|---|---|
| `main` | 팀이 검토한 결과를 모아 두는 기본 브랜치 |
| `feature/작업명` | 기능을 개발하는 임시 작업 브랜치 |
| `fix/문제명` | 오류를 고치는 임시 작업 브랜치 |
| Commit | 파일 변경 내용을 한 번 기록한 버전 |
| Push / Colab의 GitHub 저장 | 작업 브랜치 변경을 GitHub 서버에 올리는 동작 |
| Pull Request(PR) | 자신의 변경 사항을 `main`에 합치자고 요청하는 페이지 |
| Review / Approve | 다른 팀원이 변경 내역을 확인하고 승인하는 절차 |
| Merge | 검토된 작업을 기준 브랜치에 실제로 합치는 동작 |

GitHub에 Push한 **브랜치는 Repository에 접근할 수 있는 팀원 모두에게 보입니다.** 하지만 `main`에는 Merge하기 전까지 반영되지 않습니다. Colab에서 아직 GitHub에 저장하지 않은 변경 사항은 팀원에게 자동으로 공유되지 않습니다.

## 1. 담당 Issue 확인

1. GitHub Repository → `Issues`를 엽니다.
2. 자신에게 할당된 Issue의 제목과 설명, 작업 범위를 확인합니다.
3. 해당 Issue가 프로젝트 보드에 연결되어 있다면 `In Progress`로 옮깁니다.
4. 한 작업을 한 브랜치에서 진행합니다.

예: Issue `#12 Drive 데이터 불러오기` → 브랜치 `feature/drive-loading`.

## 2. GitHub에서 작업 브랜치 생성

1. Repository → `Code` 탭으로 이동합니다.
2. 파일 목록 위쪽 `main` 브랜치 선택 메뉴를 클릭합니다.
3. `feature/drive-loading`처럼 작업 이름을 입력합니다.
4. `Create branch ... from main`을 선택합니다.
5. 새로 만든 브랜치를 선택했을 때 상단에 `feature/drive-loading`이 표시되는지 확인합니다.

브랜치 이름은 `feature/` 또는 `fix/` 뒤에 소문자 영어와 하이픈을 사용하면 편리합니다. **팀원마다 이름을 정하는 것이 아니라 작업마다 이름을 정하는 것**입니다.

## 3. Colab에서 해당 브랜치의 노트북 열기

1. [Colab](https://colab.research.google.com) → `파일 → 노트북 열기 → GitHub`로 이동합니다.
2. Repository를 선택하고, 작업 브랜치가 표시되면 `feature/drive-loading`을 선택합니다.
3. 수정할 `.ipynb`를 엽니다. 새 기능이라면 자신의 작업 브랜치에 새로운 `.ipynb` 파일을 추가할 수도 있습니다.
4. 새로 만들 경우 파일명 예시: `notebooks/development/drive_loading.ipynb`.
5. 다른 팀원의 동일한 노트북을 동시에 편집하지 않도록 작업 범위를 Issue에 명확히 나눕니다.

브랜치 선택이 보이지 않는 환경에서는 GitHub의 해당 브랜치에서 `.ipynb` 파일을 열고 파일 URL을 Colab에 넣어 여는 방법을 사용합니다. **어떤 방법으로 열었든 저장할 때는 대상 브랜치를 다시 확인**합니다.

## 4. Colab에서 수정·실행 및 GitHub에 저장

1. 필요하면 노트북에서 Google Drive를 마운트합니다.
2. 맡은 기능을 `.ipynb`의 코드 셀에서 구현하고 실행 결과를 확인합니다.
3. GitHub 공개 범위와 관계없이 토큰·개인정보·대량 출력·민감한 입력 데이터가 노트북에 남지 않도록 점검합니다. 가능하면 저장 시 셀 출력은 제거합니다.
4. Colab의 `파일 → GitHub에 사본 저장(Save a copy in GitHub)`을 선택합니다.
5. Repository가 팀 저장소인지, Branch가 **자신의 `feature/...` 브랜치인지**, File path가 **원하는 노트북 경로인지** 확인합니다.
6. Commit message를 입력하고 저장합니다. 예: `Add Drive data loading notebook`.
7. GitHub 웹에서 브랜치 목록을 새로고침한 뒤 Commit이 올라왔는지 확인합니다.

**실수 방지:** GitHub에 저장할 때 `main`을 선택하면 팀 규칙을 어깁니다. 기존 노트북과 다른 경로로 저장하면 의도하지 않은 중복 파일이 생길 수 있습니다. Colab에서 런타임 파일만 수정한 것은 GitHub에 자동 반영되지 않습니다.

## 5. Pull Request 생성

1. GitHub Repository → `Pull requests` → `New pull request`를 클릭합니다.
2. 브랜치를 `base: main`, `compare: feature/drive-loading`으로 선택합니다.
3. 변경 파일과 차이를 확인합니다. 의도하지 않은 노트북/출력/자료가 포함되어 있으면 작업 브랜치에서 수정합니다.
4. 제목 예: `Add Drive data loading workflow`.
5. 설명에는 **무엇이 바뀌었는지**, **Colab에서 어떻게 실행해 확인했는지**, **관련 Issue**를 적습니다.
6. `Create pull request`를 클릭합니다.
7. 오른쪽의 `Reviewers`에서 팀원 1명을 지정합니다. 화면에서 지정이 제한되면 PR 링크를 팀원에게 전달해 검토를 요청합니다.

PR은 아직 병합이 아닙니다. `main`의 코드도 아직 바뀌지 않았습니다.

## 6. 다른 팀원이 PR을 검토하고 승인

리뷰 담당자는 다음 순서로 확인합니다.

1. GitHub → `Pull requests`에서 해당 PR을 엽니다.
2. `Files changed` 탭에서 수정된 `.ipynb` 파일·셀의 변경 사항을 확인합니다.
3. 필요하면 해당 PR의 작업 브랜치 노트북을 Colab에서 직접 열어 실행합니다. 브랜치 내용이 `main`에 반영되기 전에도 검토할 수 있습니다.
4. 문제가 없으면 `Review changes` → `Approve` → `Submit review`를 선택합니다.
5. 수정이 필요하면 `Comment` 또는 `Request changes`로 구체적인 위치와 이유를 남깁니다.

브랜치 보호 규칙이 활성화되어 있다면 요구된 승인 수를 충족하기 전까지 Merge가 차단됩니다. 규칙 강제가 없는 경우에도 팀 내부에서 같은 리뷰 절차를 지킵니다.

## 7. Merge와 브랜치 삭제

1. PR 작성자 또는 병합 담당자가 리뷰 승인과 충돌 여부를 확인합니다.
2. `Conversation` 탭 아래 병합 영역을 확인합니다.
3. `Squash and merge`가 허용되어 있다면 해당 메뉴를 선택합니다. 이는 여러 작업 Commit을 한 Commit으로 정리해서 `main`에 반영하는 방식입니다.
4. `Confirm squash and merge`를 클릭합니다.
5. PR 상태가 `Merged`로 변경되었는지 확인합니다.
6. 더 이상 쓰지 않는 브랜치는 `Delete branch`로 삭제합니다.
7. GitHub Projects 상태를 `Done`으로 옮기고 관련 Issue를 완료 처리합니다.

`main`에 병합한 내용이 다른 사람의 **기존** `feature/...` 브랜치로 자동 복사되지는 않습니다. 나머지 팀원은 자신의 작업을 병합하기 전에 최신 `main`과의 차이를 확인해야 합니다.

## 8. 다른 팀원의 변경 사항을 반영해야 할 때

예: 팀원 A의 작업이 `main`에 먼저 병합되고, 팀원 B의 작업 브랜치는 이전 `main`에서 시작한 상태입니다.

1. B는 자신의 PR을 엽니다.
2. `This branch is out-of-date` 또는 유사 안내가 표시되면 `Update branch`를 사용할 수 있는지 확인합니다.
3. 충돌이 없고 버튼이 제공되면 `Update branch`로 현재 `main`의 변경 사항을 B의 브랜치에 반영합니다.
4. 다시 Colab에서 자신의 노트북을 실행해 문제가 없는지 확인합니다.
5. 검토와 병합을 진행합니다.

반드시 `Update branch` 버튼이 표시되는 것은 아닙니다. 충돌이 있거나 저장소 규칙이 다르면 다른 해결 절차가 필요합니다.

## 9. 충돌(Conflict)이 생기면

**충돌이란?** 두 작업 브랜치가 같은 파일의 같은 부분을 서로 다르게 수정해 GitHub가 어느 쪽을 채택할지 결정하지 못하는 상태입니다.

- `.ipynb`는 내부가 JSON 형식이어서 **같은 노트북을 두 사람이 수정하면 충돌 해결이 특히 어렵습니다.** 가능하면 개발 노트북을 기능별로 분리합니다.
- PR에 `This branch has conflicts`가 뜨면 무작정 `Merge`하지 않습니다.
- 작은 Markdown/텍스트 파일 충돌은 PR의 `Resolve conflicts` 메뉴에서 수정할 수 있습니다(지원되는 충돌에 한함).
- `.ipynb` 충돌은 GitHub 웹 편집기로 무리하게 해결하기보다 **두 버전의 변경 셀을 비교한 뒤, 담당자가 최신 `main`을 기준으로 필요한 셀을 하나의 노트북에 재적용**하는 방식을 권장합니다. 완성본은 자신의 작업 브랜치에 새 Commit으로 저장하고 PR을 다시 확인합니다.
- 어느 쪽 변경을 남길지 알 수 없다면 다른 팀원과 합의한 후 수정합니다.

## 10. 2명이 서로 다른 브랜치에서 작업한 실제 예

| 순서 | 팀원 A | 팀원 B | `main` |
|---|---|---|---|
| 1 | `feature/drive-loading` 생성 | `feature/result-view` 생성 | 기존 상태 |
| 2 | `development/drive_loading.ipynb` 작업 | `development/result_view.ipynb` 작업 | 기존 상태 |
| 3 | Colab에서 자신의 브랜치에 저장 | Colab에서 자신의 브랜치에 저장 | 기존 상태 |
| 4 | PR 생성 → 동료 승인 → Merge | 개발 진행 | A의 노트북만 반영 |
| 5 | 브랜치 삭제 | 최신 `main` 반영 후 PR 생성 | A 반영 상태 |
| 6 | B의 PR 리뷰 | 승인 후 Merge, 브랜치 삭제 | A와 B의 노트북 모두 반영 |

이후 서비스 담당자는 **최신 `main` 기준의 작업 브랜치**를 만들고 `notebooks/service/`에 자신의 시연 노트북을 구성합니다.

## 11. 작업 전후 체크리스트

- [ ] Issue에서 담당 기능과 노트북을 확인함
- [ ] `main`을 기준으로 작업 브랜치를 생성함
- [ ] Colab에서 올바른 브랜치의 노트북을 열었음
- [ ] GitHub 저장 시 Repository·브랜치·경로를 확인함
- [ ] 저장한 Commit이 GitHub의 작업 브랜치에 보임
- [ ] PR에서 `base: main` / `compare: 작업 브랜치`를 확인함
- [ ] 동료가 검토하고 승인함
- [ ] 병합 후 `main` 변경 사항을 확인하고 작업 브랜치를 정리함

## 공식 참고 자료

- [Pull Request 만들기](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/creating-a-pull-request)
- [PR 병합하기](https://docs.github.com/en/pull-requests/how-tos/merge-and-close-pull-requests/merging-a-pull-request)
- [PR 브랜치 업데이트](https://docs.github.com/en/pull-requests/how-tos/create-pull-requests/keeping-your-pull-request-in-sync-with-the-base-branch)
- [Colab과 GitHub 연동 예시](https://github.com/googlecolab/colabtools/blob/master/notebooks/colab-github-demo.ipynb)
