# RENAME_ME_PROJECT — Colab 팀 프로젝트

Google Colab의 `.ipynb`를 중심으로 개발하고, GitHub에서 브랜치·Pull Request로 협업하는 프로젝트 저장소입니다. 모델·데이터셋과 구현 기술은 프로젝트 진행 중 결정합니다.

## 시작 순서

1. 관리자가 `docs/TEAM_ENVIRONMENT_INFO.md`의 실제 Organization·Repository·Google Drive 폴더 정보를 채웁니다.
2. 팀원은 `docs/TEAM_COMMON_SETUP.md`를 따라 **개인 Google Drive**에 이 GitHub 저장소 전체를 한 번 Clone합니다.
3. 개발할 때는 Drive 안의 `repository/notebooks/` 파일을 열어 작업하고, **해당 파일이 그 경로에 저장되었는지 확인**합니다.
4. 현재 작업 노트북과 연결된 원격 Linux 터미널에서 `git status` → `git add` → `git commit` → `git push`를 수행합니다.
5. GitHub에서 Pull Request를 생성해 검토받고 `main`에 병합합니다.
6. 용량이 큰 데이터·모델·체크포인트는 팀의 **공동 Google Drive 폴더**에서 사용하고, 버전·위치는 `docs/DATA_MODEL_REGISTRY.md`에 기록합니다.
7. 웹 시연은 `notebooks/service/`의 노트북에서 서버를 실행하고 ngrok으로 접속합니다.

## 문서

- `STRUCTURE.md` — 모든 폴더·파일의 역할, 실제 사용 예시, 이름 변경 기준
- `docs/TEAM_ENVIRONMENT_INFO.md` — 팀에 전달할 확정된 설정 **결과**
- `docs/TEAM_COMMON_SETUP.md` — 팀원이 진행할 공통 초기 설정
- `docs/TEAM_GIT_WORKFLOW.md` — 브랜치 생성·수정·Push·PR·병합·충돌 해결
- `docs/GOOGLE_DRIVE_LARGE_FILES.md` — 대용량 파일 공유 및 Drive 버전 관리
- `docs/DATA_MODEL_REGISTRY.md` — 데이터·모델 버전 정보 기록표
- `docs/NGROK_WEB_DEMO.md` — ngrok 웹 시연 단계
- `docs/PORTFOLIO_AND_REPRODUCTION.md` — 결과 기록과 포트폴리오 재현 정보

## 이름을 바꿀 항목

`RENAME_ME_`로 시작하는 값은 실제 정보를 채워 넣는 자리입니다. `RENAME_ME_PROJECT`는 이 ZIP의 **최상위 폴더 이름**이며, `repository`는 Git 저장소를 Clone할 폴더 이름으로 문서 전체에서 통일한 예시입니다. 각각을 임의로 바꾸면 모든 경로도 함께 바꾸십시오.

> 노트북·설명서·작은 공개 예제는 GitHub로 관리합니다. 대용량 데이터·모델은 Drive에 저장하며 GitHub 안에 중복해서 넣지 않습니다. 인증정보는 GitHub에 저장하지 않습니다.
