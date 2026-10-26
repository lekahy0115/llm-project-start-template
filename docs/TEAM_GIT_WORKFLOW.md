# GitHub 브랜치 협업 — 팀원별 실제 작업 순서

모든 Git 명령은 **현재 열려 있는 노트북과 같은 Colab 런타임의 Linux 터미널**에서 실행합니다. 어느 노트북의 특정 셀에서 명령을 실행해야 하는 것이 아닙니다.

**Git 저장소 작업 경로:**

```text
/content/drive/MyDrive/RENAME_ME_PROJECT/repository/
```

## 1. 작업 시작: 최신 main에서 브랜치 만들기

GitHub Issues에서 담당 작업을 확인합니다. 예를 들어 데이터 입력 기능을 맡았다면 브랜치명을 `feature/data-input`으로 정합니다.

```bash
cd /content/drive/MyDrive/RENAME_ME_PROJECT/repository
git switch main
git pull --ff-only origin main
git switch -c feature/data-input
```

이미 같은 작업 브랜치가 있으면 `git switch feature/data-input`으로 이동합니다. 원격 브랜치까지 공유하려면 최초 Push 때 `-u`를 사용합니다.

**브랜치 전환 전**에는 열린 노트북을 저장하고 닫고, 전환 후 해당 브랜치의 파일을 다시 열어야 합니다. 브랜치 전환은 저장소 파일 내용을 바꿀 수 있습니다.

## 2. 실제 개발: Git 저장소 안의 파일 사용

개발할 파일 예시:

```text
/content/drive/MyDrive/RENAME_ME_PROJECT/repository/notebooks/development/data_input.ipynb
```

Drive 웹사이트에서 해당 파일을 열거나, 새 `.ipynb`를 `notebooks/development/`에 생성·이동하여 엽니다. 편집기에서 저장한 뒤 Linux 터미널에서 변경을 확인합니다.

```bash
cd /content/drive/MyDrive/RENAME_ME_PROJECT/repository
git branch --show-current
git status --short
```

`feature/data-input`이 현재 브랜치로 나오고 `notebooks/development/data_input.ipynb`가 변경/추가 파일로 표시되어야 합니다.

## 3. Commit·Push: 내 브랜치에만 반영

```bash
git add notebooks/development/data_input.ipynb
git diff --cached --stat
git commit -m "Implement data input notebook"
git push -u origin feature/data-input
```

다른 파일도 작업했다면 **실제로 추가할 파일만** `git add 파일경로`로 추가합니다. 무조건 `git add .`를 실행하기 전에 `git status`로 개인정보·대용량 파일 포함 여부를 확인합니다.

`git push`는 원격 GitHub에 변경 사항을 올리는 작업이고, `git pull`은 원격 변경 사항을 가져와 현재 브랜치에 통합하는 작업입니다.

## 4. Pull Request 만들기·병합

1. GitHub 저장소 → `Pull requests` → `New pull request` 선택
2. `base: main`, `compare: feature/data-input` 확인
3. 변경 설명과 관련 Issue를 적고 PR 생성
4. 다른 팀원이 `Files changed`를 검토하고 문제가 없으면 승인 (`Approve`)
5. 팀 규칙과 보호 규칙을 충족하면 `Squash and merge` → 확인
6. 병합 완료 후 원격 작업 브랜치를 삭제

PR을 병합했다고 다른 팀원의 기존 기능 브랜치가 자동 갱신되지는 않습니다.

## 5. 병합 후 새 작업

같은 런타임 Linux 터미널에서, 수정 중인 파일을 저장한 상태로:

```bash
cd /content/drive/MyDrive/RENAME_ME_PROJECT/repository
git switch main
git pull --ff-only origin main
git switch -c feature/RENAME_ME_NEXT_FEATURE
```

이미 합쳐진 자신의 기존 브랜치는 필요 없으면 `git branch -d feature/data-input`으로 삭제합니다.

## 6. 다른 팀원의 변경을 지금 내 브랜치에 반영하려면

진행 중인 작업을 Commit한 다음:

```bash
git fetch origin
git switch feature/data-input
git merge origin/main
```

충돌이 없으면 병합 완료입니다. 충돌이 나면 Git이 어느 파일이 충돌했는지 표시합니다.

## 7. 충돌이 발생하면

1. `git status`로 충돌 파일 확인
2. 충돌 파일을 열어 필요한 내용을 합침 (`<<<<<<<`, `=======`, `>>>>>>>` 표시가 있다면 해결)
3. `.ipynb`는 JSON 구조라 웹 편집기만으로 해결하기 어려울 수 있으므로 해당 파일을 누가 수정했는지 팀원과 확인하고, 필요한 경우 한쪽 노트북의 셀을 다른 노트북에 수동 병합
4. 해결한 파일을 `git add 파일경로`로 등록하고 `git commit`하여 완료
5. 실행 결과를 확인한 후 Push하고 PR 갱신

잘못된 병합을 시작했지만 아직 완료하지 않았다면 `git merge --abort`로 중단할 수 있습니다.

## 8. 4명 협업 예시

| 팀원 | 브랜치 | 수정 파일 예시 |
|---|---|---|
| A | `feature/data-input` | `notebooks/development/data_input.ipynb` |
| B | `feature/model-loading` | `notebooks/development/model_loading.ipynb` |
| C | `feature/evaluation` | `notebooks/evaluation/quality_check.ipynb` |
| D | `feature/web-demo` | `notebooks/service/service_demo.ipynb` |

각자가 별도의 브랜치와 노트북에서 작업하고, PR을 순서대로 `main`에 병합합니다. 병합 전에 최신 `main`을 확인하고, 같은 파일을 동시에 수정했다면 충돌을 조정합니다.

참고: https://docs.github.com/en/pull-requests · https://git-scm.com/docs/git-switch · https://git-scm.com/docs/git-merge

## 팀원 공통 작업 전·후 체크리스트

### 작업 전
- [ ] GitHub Issues에서 담당 작업과 파일 범위를 확인합니다.
- [ ] **현재 편집 중인 노트북을 저장하고 닫은 후** Git 브랜치를 생성·전환합니다.
- [ ] `git branch --show-current`로 본인 브랜치를 확인합니다.
- [ ] Drive 웹사이트에서 해당 브랜치의 실제 `repository/notebooks/...` 파일을 다시 엽니다.

### 작업 후
- [ ] 파일이 개인 Git 저장소 내부의 실제 Drive 경로에 저장되었는지 확인합니다.
- [ ] `git status --short`에서 의도한 변경만 표시되는지 확인합니다.
- [ ] API 키, 인증 토큰, 개인 정보, 대용량 모델 파일을 Commit하지 않았는지 확인합니다.
- [ ] Push 대상 브랜치와 PR의 `base: main`, `compare: feature/...`를 확인합니다.
- [ ] 병합 후 `main`의 최신 변경 사항을 가져오기 전에 열려 있는 노트북을 닫습니다.

## 충돌을 줄이는 작업 규칙
- 서로 다른 브랜치라도 **같은 `.ipynb` 파일을 동시에 수정하면** PR 병합 시 충돌이 날 수 있습니다. 작업을 Issues에서 분담하고 노트북 파일을 기능별로 구분합니다.
- 브랜치 전환·병합 도중 열린 노트북이 이전 상태를 다시 저장하지 않도록 **저장 → 닫기 → Git 작업 → 다시 열기** 순서를 유지합니다.
- `git pull origin main`을 본인 `feature/*` 브랜치에서 바로 실행하면 `main` 변경을 해당 기능 브랜치에 통합하는 동작이 됩니다. 새로운 기능 작업 시작 시에는 먼저 `main`으로 전환하여 `git pull --ff-only origin main`을 실행합니다.
- 브랜치 이름은 팀원 이름으로 고정하지 않습니다. 기능·수정 작업 단위로 만들고 병합 후 정리합니다.

## 공식 문서
- GitHub PR 생성: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request
- GitHub 리뷰: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/reviewing-proposed-changes-in-a-pull-request
- Git 병합: https://git-scm.com/docs/git-merge
