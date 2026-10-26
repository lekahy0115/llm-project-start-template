# 팀원 공통 초기 설정 — GitHub + Drive + Colab

## 준비할 것

- Organization의 해당 Public Repository를 볼 수 있는 GitHub 계정
- 본인 Google 계정과 저장 공간
- `TEAM_ENVIRONMENT_INFO.md`에 적힌 실제 이름·경로
- GitHub에 Push할 팀원은 Repository **Write** 권한

## 1. Drive에 개인 Git 저장소 위치 준비

Drive 웹사이트(`https://drive.google.com`)에서 `내 드라이브/RENAME_ME_PROJECT/` 폴더를 만듭니다. `repository/`는 Clone 명령이 생성하므로 미리 만들지 않습니다.

개인별 예상 경로:

```text
/content/drive/MyDrive/RENAME_ME_PROJECT/repository/
```

이 경로는 Git 명령의 **작업 디렉터리**이고, 팀원의 개인 Git 저장소 복제본입니다. 팀원끼리 이 폴더를 공유하지 않습니다.

## 2. Drive 연결 (최초 한 번 진행 후 세션마다 재마운트 가능)

1. `https://colab.research.google.com`에서 새 노트북을 열거나, GitHub의 `notebooks/00_environment_check.ipynb`를 엽니다.
2. 실행 코드 셀에서 다음을 실행합니다.

```python
from google.colab import drive
drive.mount('/content/drive')
```

3. Google 계정으로 인증한 후 `/content/drive/MyDrive/RENAME_ME_PROJECT/`가 존재하는지 확인합니다.

이 첫 노트북은 **Drive 연결을 위한 진입 화면**이며, Git 동기화용 파일을 새로 만드는 절차는 아닙니다.

## 3. GitHub 저장소 전체 Clone (최초 1회)

Drive 마운트가 완료된 **같은 런타임의 Linux 터미널**을 열고 다음을 실행합니다.

```bash
git clone https://github.com/RENAME_ME_ORG/RENAME_ME_REPOSITORY.git \
  /content/drive/MyDrive/RENAME_ME_PROJECT/repository
cd /content/drive/MyDrive/RENAME_ME_PROJECT/repository
git status
```

`On branch main` 등이 보이면 저장소로 인식한 것입니다. 이미 Clone한 이후에는 다시 Clone하지 않습니다.

## 4. 공용 대용량 폴더 접근

팀에서 공유받은 `RENAME_ME_SHARED_DATA` 폴더를 Drive의 `공유 문서함`에서 찾습니다. 우클릭 → `정리` → `바로가기 추가`로 `내 드라이브` 최상위에 같은 이름으로 추가합니다.

정상 경로 예시:

```text
/content/drive/MyDrive/RENAME_ME_SHARED_DATA/datasets/raw/v001/
```

공용 대용량 파일 사용·버전 규칙은 `GOOGLE_DRIVE_LARGE_FILES.md`를 따릅니다.

## 5. Drive에 있는 노트북을 실제로 열기

Drive 웹사이트에서 **`내 드라이브/RENAME_ME_PROJECT/repository/notebooks/`**의 `.ipynb` 파일을 선택해 Google Colaboratory로 엽니다. GitHub 웹 URL에서 노트북을 열면 개인 Drive의 Git 저장소 파일과 자동으로 연결되지 않습니다.

새 노트북은 Git 저장소 안의 `notebooks/development/` 또는 다른 해당 폴더에 생성/이동한 뒤 엽니다. 새 노트북이 기본 `Colab Notebooks/`에 생성되었다면 Drive 웹사이트에서 저장소 폴더로 이동하고 **이동한 파일을 다시 엽니다.**

파일을 수정하고 저장한 다음 Linux 터미널에서 다음을 확인합니다.

```bash
cd /content/drive/MyDrive/RENAME_ME_PROJECT/repository
git status --short
```

수정한 노트북이 표시되지 않으면 **편집 중인 파일과 Git 저장소 파일이 서로 다른 것**일 수 있으므로 저장·경로를 확인하십시오.

## 6. GitHub에 Push할 계정 인증 (개인별 1회 준비)

GitHub 계정의 `Settings → Developer settings → Personal access tokens → Fine-grained tokens`에서 사용할 Repository만 선택하고 **Contents: Read and write** 권한의 토큰을 발급할 수 있습니다. Organization 정책이 있다면 해당 승인도 필요합니다.

이후 Linux 터미널에서 `git push` 인증을 요청할 때 GitHub 사용자명과 토큰을 사용합니다. **토큰을 노트북·README·명령어 URL·Drive 공개 파일에 기록하지 마십시오.** 토큰은 GitHub 계정 비밀번호가 아닙니다.

최초 Commit 전에 본인 Git 작성자 정보를 지정합니다.

```bash
git config --global user.name "RENAME_ME_GITHUB_DISPLAY_NAME"
git config --global user.email "RENAME_ME_GITHUB_EMAIL"
```

GitHub에서 비공개 이메일을 사용한다면 GitHub가 제공하는 `noreply` 주소를 설정해도 됩니다. `--global` 설정은 새 런타임에서 다시 필요할 수 있습니다.

## 7. 작업 시작

`TEAM_GIT_WORKFLOW.md`의 순서대로 `main` 갱신 → 브랜치 생성 → `.ipynb` 작업 → Commit·Push → PR·Merge를 수행합니다.

### 확인 항목

- [ ] 개인 Drive의 `repository/.git/` 경로가 존재함
- [ ] 현재 Git 브랜치가 확인됨
- [ ] 공용 Drive 대용량 폴더를 읽을 수 있음
- [ ] Drive에서 연 노트북 수정이 Git `status`에 나타남
- [ ] 본인 브랜치에 Push할 GitHub 권한이 있음

참고: https://research.google.com/colaboratory/faq.html · https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens

## 처음 설정할 때의 실제 순서와 확인 기준

1. 팀 공통 정보 문서에서 Organization, Repository, 개인 Drive 상위 폴더명, 공용 대용량 파일 폴더명을 확인합니다.
2. 본인 Drive의 `RENAME_ME_PROJECT/` 폴더를 생성합니다. `repository/` 폴더는 미리 만들지 않습니다.
3. Drive 마운트를 완료합니다. `00_environment_check.ipynb`가 GitHub에만 존재할 때는, **Clone 전의 연결용 노트북**으로 GitHub에서 열어 실행할 수 있지만 이 화면에서 편집한 내용이 Drive 저장소에 자동 반영되지는 않습니다.
4. **최초 Clone 전** 환경 점검 노트북에서 `개인 Git 저장소: ... 존재: False`가 보이는 것은 정상입니다. 공용 폴더도 생성·바로가기 추가 전이면 `False`입니다.
5. 마운트 후 Linux 터미널에서 Clone을 진행합니다. Clone이 성공한 뒤 `repository/.git/`과 `repository/notebooks/`가 있는지 확인합니다.
6. 이후에는 **Drive 웹사이트의** `내 드라이브/RENAME_ME_PROJECT/repository/notebooks/00_environment_check.ipynb` 파일을 Colaboratory로 열어 검사하면 Repository 존재가 `True`여야 합니다.
7. 저장 확인용으로 작업 브랜치에서 작은 `.ipynb` 파일을 수정하고 저장한 뒤 `git status --short`로 해당 파일 변경을 확인합니다. 테스트 수정은 본인의 작업 브랜치에서만 진행합니다.

**검사 실패 시 구분:** Drive 경로가 없으면 폴더명·마운트를, Git 저장소만 없으면 Clone 완료 여부를, Git 변경 내역이 없으면 수정한 `.ipynb`의 실제 Drive 경로를 확인합니다. GitHub에 Push할 때 403 오류가 발생하면 본인 GitHub 계정의 Write 권한과 인증을 확인합니다.

**GitHub 로그인과 Git Push 인증은 다릅니다.** Public Repository의 읽기·Clone은 인증 없이 가능하지만, Push에는 권한과 인증이 필요합니다. 개인 액세스 토큰을 셀에 하드코딩하거나 터미널 명령 URL에 넣지 않습니다. 일부 Colab 계정에서는 터미널 메뉴를 사용할 수 없으며 그 경우 별도 셀에서 `%cd`, `!git`로 대체할 수 있습니다. 이 방법은 계정별 UI 차이를 설명하는 대안이지, Git 전용 노트북을 새로 만드는 절차가 아닙니다.

## 참고 문서
- Google Colab FAQ: https://research.google.com/colaboratory/faq.html
- GitHub 인증 토큰: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens
- Git 클론: https://git-scm.com/docs/git-clone
