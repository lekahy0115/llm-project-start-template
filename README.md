# Google Colab 기반 LLM 팀 프로젝트

Google Colab의 **`.ipynb` 노트북**을 중심으로 LLM 기능을 개발·평가하고, 같은 Colab 환경에서 시연용 웹 서비스를 실행하는 GitHub 협업 저장소입니다. 팀원 4명이 기능별 브랜치에서 작업하고 Pull Request로 변경 사항을 통합합니다. 데이터·모델 가중치·대용량 결과물은 Google Drive에서 관리합니다.

## 저장소 이용 순서

1. [`docs/TEAM_ENVIRONMENT_INFO.md`](docs/TEAM_ENVIRONMENT_INFO.md)에서 팀 공통 주소·브랜치 규칙·Drive 폴더명을 확인합니다.
2. [`docs/TEAM_COMMON_SETUP.md`](docs/TEAM_COMMON_SETUP.md)를 따라 GitHub·Colab·Drive 접근을 설정합니다.
3. [`notebooks/00_COLAB_CONNECTION_CHECK.ipynb`](notebooks/00_COLAB_CONNECTION_CHECK.ipynb)를 Colab에서 열고 Drive 연동을 확인합니다.
4. [`docs/TEAM_COLLABORATION_WORKFLOW.md`](docs/TEAM_COLLABORATION_WORKFLOW.md)를 참고해 작업 브랜치를 만들고, 노트북을 저장하고, PR로 병합합니다.
5. 서비스 시연은 [`docs/SERVICE_DEMO.md`](docs/SERVICE_DEMO.md)를 참고합니다.

## 저장 장소 구분

| 장소 | 저장할 내용 | 저장하지 않을 내용 |
|---|---|---|
| GitHub | `.ipynb`, 문서, 공개 가능한 작은 예제, 설정 파일 | 토큰·비밀번호·개인정보·대용량 모델 |
| Google Drive | 원본/가공 데이터, 모델 가중치, 체크포인트, 대용량 결과물 | GitHub에 제출할 협업 기록·PR |
| Colab 런타임(`/content`) | 현재 세션에서 실행하는 코드와 임시 파일 | 장기간 보존해야 하는 유일한 원본 |

## 폴더와 이름

폴더별 역할과 이름 변경 기준은 [`STRUCTURE.md`](STRUCTURE.md)에 설명되어 있습니다. 프로젝트명을 확정하면 ZIP 최상위 `RENAME_ME_PROJECT_NAME` 폴더를 실제 프로젝트명으로 변경합니다. GitHub Repository명은 별도로 지정할 수 있습니다.

## 범위

이 저장소에는 LLM 모델·RAG·학습 파이프라인·웹 UI의 구현 코드는 들어 있지 않습니다. 프로젝트 주제가 정해지면 `notebooks/development/`, `notebooks/evaluation/`, `notebooks/service/`에 작업별 `.ipynb` 파일을 생성합니다. 필요한 경우에만 별도 Python 모듈 구조를 추가할 수 있습니다.
