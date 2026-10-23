# 팀원 공통 환경 설정: GitHub · Google Colab · Google Drive

모든 팀원이 자신의 계정에서 **최초 1회** 진행하는 연결 설정과 확인 방법입니다. GitHub 조직 생성·Repository 관리자 설정은 포함하지 않습니다.

## 1. 사용할 계정 준비

1. GitHub 계정과 Google 계정으로 각각 로그인합니다.
2. 팀에서 전달받은 [`TEAM_ENVIRONMENT_INFO.md`](TEAM_ENVIRONMENT_INFO.md)의 Repository 주소, 공개 범위, Google Drive 공유 폴더 이름을 확인합니다.
3. GitHub Organization/Repository 초대가 온 경우 초대 링크를 열어 수락합니다. Private Repository라면 초대를 수락해야 접근할 수 있습니다.
4. Repository 주소를 열어 `README.md`, `notebooks/`, `docs/`가 표시되는지 확인합니다.

**확인 결과:** Repository 파일 목록을 볼 수 있어야 합니다. 접근 불가 메시지가 나오면 Organization 멤버십과 Repository 권한을 확인해야 합니다.

## 2. Google Drive 공유 폴더 접근 설정

1. 팀에서 전달받은 공유 폴더 링크를 열고 접근 권한이 있는지 확인합니다.
2. [Google Drive](https://drive.google.com) → 왼쪽 `공유 문서함(Shared with me)`으로 이동합니다.
3. 팀의 `RENAME_ME_SHARED_DRIVE_FOLDER` 폴더를 찾습니다.
4. 폴더를 우클릭하고 `정리(Organize)` → `바로가기 추가(Add shortcut)`를 선택합니다.
5. 목적지를 **내 드라이브(My Drive) 최상위**로 지정합니다.
6. 바로가기 이름이 팀 안내에 적힌 `RENAME_ME_SHARED_DRIVE_FOLDER`와 **완전히 동일한지** 확인합니다. 이름이 다르면 팀 표준 이름으로 바꿉니다.
7. `내 드라이브`에 해당 바로가기가 표시되고, 내부의 `datasets/`, `models/`, `outputs/` 등 폴더가 열리는지 확인합니다.

**왜 바로가기가 필요한가요?** 공유 문서함에 보인다는 사실만으로 Colab의 `/content/drive/MyDrive/`에 같은 경로가 생기지는 않습니다. 바로가기를 `내 드라이브`에 만들어야 팀 공통 경로로 접근하기 쉽습니다.

**주의:** 바로가기 생성과 원본 폴더 접근 권한은 별개입니다. 권한이 없으면 폴더 소유자에게 공유 권한을 요청해야 합니다.

## 3. Colab에서 연결 확인 노트북 열기

1. [Google Colab](https://colab.research.google.com)에 로그인합니다.
2. `파일(File)` → `노트북 열기(Open notebook)`를 선택합니다.
3. `GitHub` 탭을 선택합니다. 처음이라면 GitHub 계정 접근 권한을 승인합니다.
4. Organization 또는 Repository 주소를 이용해 해당 저장소를 찾습니다.
5. `notebooks/00_COLAB_CONNECTION_CHECK.ipynb`를 선택합니다.
6. 열리지 않으면 GitHub Repository에서 노트북 파일을 열고 `Open in Colab` 버튼이 있으면 선택하거나, Colab의 `GitHub` 탭에 해당 GitHub 노트북 URL을 입력합니다.
7. `런타임(Runtime)` → `런타임 유형 변경(Change runtime type)`에서 Python 런타임을 선택합니다. GPU는 지금 필요하지 않으므로 CPU로 시작해도 됩니다.

**확인 결과:** Google Colab 편집기에서 연결 확인용 `.ipynb`가 열려야 합니다.

Private Repository는 Colab의 GitHub 연결 권한/Private 저장소 접근을 추가로 허용해야 목록에 나올 수 있습니다. 초대 수락과 GitHub 인증이 필요합니다.

## 4. Google Drive 마운트 및 경로 검증

노트북 첫 번째 실행 셀에서 다음 명령을 실행합니다.

```python
from google.colab import drive
drive.mount('/content/drive')
```

1. 표시된 Google 인증 화면에서 자신의 Google 계정을 선택합니다.
2. Drive 접근을 허용합니다.
3. 다음 셀에서 `DRIVE_FOLDER_NAME`의 문자열 `RENAME_ME_SHARED_DRIVE_FOLDER`를 **팀에서 전달받은 실제 폴더명**으로 변경합니다.
4. 셀을 실행해 `폴더 존재: True`와 데이터/모델/결과 폴더의 존재 여부를 확인합니다.

예상 경로:

```text
/content/drive/MyDrive/RENAME_ME_SHARED_DRIVE_FOLDER/datasets/raw
/content/drive/MyDrive/RENAME_ME_SHARED_DRIVE_FOLDER/datasets/processed
/content/drive/MyDrive/RENAME_ME_SHARED_DRIVE_FOLDER/models
/content/drive/MyDrive/RENAME_ME_SHARED_DRIVE_FOLDER/checkpoints
/content/drive/MyDrive/RENAME_ME_SHARED_DRIVE_FOLDER/outputs
```

**오류 해결:** `False`라면 Drive 폴더명 오타, `내 드라이브` 바로가기 누락, 공유 권한 미설정, 잘못된 Google 계정으로 마운트한 경우를 확인합니다. Drive 공유 경로가 확인되기 전에는 데이터 파일을 임의 위치에 복사하지 않습니다.

## 5. GitHub 브랜치에서 Colab 파일 열기와 저장 권한 확인

1. GitHub Repository → 브랜치 선택 메뉴에서 현재 작업 브랜치를 확인합니다.
2. Colab `파일 → 노트북 열기 → GitHub`에서 **작업할 브랜치의 노트북**을 선택해 엽니다. 기존 파일이 아니라 새 노트북을 시작해도 됩니다.
3. 내용을 수정한 후 Colab에서 `파일(File)` → `GitHub에 사본 저장(Save a copy in GitHub)`을 선택합니다.
4. 최초 1회라면 GitHub 쓰기 권한을 승인합니다.
5. 저장 대화상자에서 **Repository, Branch, 파일 경로**를 반드시 확인합니다. `main`이 아니라 본인의 `feature/...` 또는 `fix/...` 브랜치를 선택합니다.
6. 저장할 기존 노트북과 동일한 경로를 지정하거나, 새 노트북이면 담당 기능에 맞는 경로를 지정합니다.
7. Commit message(예: `Add first notebook cell`)를 입력하고 저장합니다.
8. GitHub 웹에서 해당 브랜치를 선택하고 새 Commit과 노트북 변경 사항이 보이는지 확인합니다.

**가장 중요한 구분:** Colab의 일반 `저장(Ctrl+S)`과 `GitHub에 사본 저장`은 동일한 동작이 아닙니다. GitHub에 변경을 남기려면 대상 브랜치에 별도로 저장해야 합니다. GitHub에서 연 노트북은 Colab 안에서 편집한다고 원본이 실시간으로 바뀌지 않습니다.

Colab GitHub 저장 대화상자에 브랜치가 없으면 GitHub에서 먼저 브랜치를 생성한 뒤 노트북을 다시 열거나 다시 시도합니다. Organization 정책 때문에 쓰기 권한 승인이 차단되면 저장소 관리자에게 확인합니다.

## 6. 환경 설정 완료 기준

- [ ] GitHub Repository의 노트북과 문서 열기 가능
- [ ] 자신의 Google Drive `내 드라이브`에서 팀 공유 폴더 바로가기 확인
- [ ] `00_COLAB_CONNECTION_CHECK.ipynb`에서 Drive 경로 확인 성공
- [ ] 자신이 생성한 작업 브랜치를 GitHub에서 볼 수 있음
- [ ] Colab에서 작업 브랜치에 노트북 저장 후 GitHub Commit 확인 가능

브랜치 생성, 팀원 리뷰, 병합은 [`TEAM_COLLABORATION_WORKFLOW.md`](TEAM_COLLABORATION_WORKFLOW.md)를 따릅니다.

## 공식 참고 자료

- [Google Colab FAQ](https://research.google.com/colaboratory/faq.html?hl=ko)
- [Google Colab의 GitHub 노트북 열기/저장 예시](https://github.com/googlecolab/colabtools/blob/master/notebooks/colab-github-demo.ipynb)
- [Google Drive 공유 폴더 바로가기 안내](https://support.google.com/drive/answer/2375057?hl=ko)
