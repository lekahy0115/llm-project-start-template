# 프로젝트 폴더 및 파일 설명

## GitHub 저장소 트리

```text
RENAME_ME_PROJECT/                # ZIP의 최상위 이름 — 실제 프로젝트명으로 변경 가능
├── .github/
│   └── README.md                # GitHub 관리 파일을 향후 어디에 둘지 설명
├── notebooks/
│   ├── README.md                # 노트북 저장 규칙
│   ├── 00_environment_check.ipynb # 처음 접속 시 Drive 마운트 및 경로 확인
│   ├── development/
│   │   └── README.md            # 기능 개발·실험 노트북
│   ├── evaluation/
│   │   └── README.md            # 평가 노트북
│   └── service/
│       └── README.md            # 서비스·ngrok 시연 노트북
├── data/
│   ├── README.md                # GitHub 파일과 Drive 대용량 파일 구분
│   └── samples/
│       └── README.md            # 공개 가능한 소규모 예제 데이터
├── configs/
│   └── README.md                # 나중에 정해질 모델·실험 설정
├── outputs/
│   └── README.md                # 작고 공유 가능한 평가·시연 결과
├── assets/
│   └── README.md                # UI 캡처·프로젝트 다이어그램
├── docs/
│   ├── README.md                # 문서 안내
│   ├── TEAM_ENVIRONMENT_INFO.md  # 관리자 설정의 결과만 기록
│   ├── TEAM_COMMON_SETUP.md     # 모든 팀원의 초기 설정 절차
│   ├── TEAM_GIT_WORKFLOW.md     # Git·브랜치·병합 단계
│   ├── GOOGLE_DRIVE_LARGE_FILES.md # 대용량 Drive 사용법
│   ├── DATA_MODEL_REGISTRY.md   # 대용량 파일 버전·경로 기록
│   ├── NGROK_WEB_DEMO.md       # ngrok 시연 절차
│   └── PORTFOLIO_AND_REPRODUCTION.md # 공개·재현 안내
├── .gitignore                   # 인증정보·캐시·대형 가중치 제외
├── README.md                    # 프로젝트 시작 방법
└── STRUCTURE.md                 # 현재 문서
```

## 각 폴더의 목적과 예시

| 경로 | 목적 | 나중에 추가할 수 있는 파일 예시(미생성) |
|---|---|---|
| `.github/` | GitHub 운영 관련 문서·설정 | 추후 필요 시 협업 규칙 파일 |
| `notebooks/development/` | 기능별 `.ipynb` 개발 | `RENAME_ME_FEATURE.ipynb` → `news_summary.ipynb` |
| `notebooks/evaluation/` | 결과·성능 검증 | `summary_quality.ipynb` |
| `notebooks/service/` | 웹 UI와 ngrok 시연 실행 | `service_demo.ipynb` |
| `data/samples/` | Git으로 관리할 **작은 공개 예제** | `example_inputs.csv` |
| `configs/` | 실험 설정을 별도 파일로 분리할 때 사용 | `experiment_v1.yaml` |
| `outputs/` | GitHub에 기록할 작은 표·정리 결과 | `metrics_summary.csv` |
| `assets/` | README에 사용할 시각 자료 | `service_screenshot.png` |
| `docs/` | 팀 협업·재현·운영 설명서 | `DATA_MODEL_REGISTRY.md` |

예시 파일명은 구현을 강제하지 않습니다. 프로젝트에서 사용할 모델·RAG·파인튜닝·웹 UI 방식은 사전에 확정하지 않습니다.

## Drive는 두 종류의 공간

**팀원별 Git 저장소** (각자의 Drive에 독립적으로 존재):

```text
/content/drive/MyDrive/RENAME_ME_PROJECT/repository/
  ├── .git/
  ├── notebooks/
  ├── data/
  └── ...
```

**공용 대용량 파일** (소유자 Drive 원본 하나를 공유, 다른 팀원은 바로가기):

```text
/content/drive/MyDrive/RENAME_ME_SHARED_DATA/
  ├── datasets/raw/v001/
  ├── datasets/processed/v001/
  ├── models/v001/
  ├── checkpoints/v001/
  └── outputs/v001/
```

`RENAME_ME_PROJECT`, `RENAME_ME_SHARED_DATA`는 각자가 합의한 실제 이름으로 **일관되게 바꾸어야 합니다.** `repository`는 한 저장소를 가리키는 예시 폴더명입니다.

GitHub Commit의 버전과 Google Drive 대용량 파일의 버전은 별개이므로 `docs/DATA_MODEL_REGISTRY.md`에 연결 관계를 남깁니다.

## 파일별 역할

- `.gitignore`: 인증정보·임시 파일·대형 모델 가중치가 Git에 올라가지 않도록 합니다. `data/samples/`의 공개 예제 파일은 무시하지 않습니다.
- `00_environment_check.ipynb`: Drive 연결과 **기대 경로 존재 여부만 검사**합니다. Git 동기화나 LLM 기능을 구현하지 않습니다.
- 각 `README.md`: 해당 위치에 어떤 파일을 놓는지 설명합니다.
- `TEAM_ENVIRONMENT_INFO.md`: Organization 이름 등 관리자가 확정한 **설정 결과**를 전달합니다. 관리자용 클릭 절차는 포함하지 않습니다.
- `TEAM_COMMON_SETUP.md`: 팀원들이 로그인·Clone·개인/공용 Drive 경로를 준비하는 방법입니다.
- `TEAM_GIT_WORKFLOW.md`: 브랜치를 다룰 때 사용하는 정확한 디렉터리와 Git 명령을 설명합니다.
- `GOOGLE_DRIVE_LARGE_FILES.md`, `DATA_MODEL_REGISTRY.md`: 대용량 파일의 저장·공유·버전 규칙을 설명합니다.
- `NGROK_WEB_DEMO.md`: 선택한 UI 서버를 ngrok에 연결하는 단계입니다.
- `PORTFOLIO_AND_REPRODUCTION.md`: Public GitHub만으로 이해할 수 있도록 결과·출처·기여도를 정리합니다.

별도 `.py` 코드·Python 패키지·Git 동기화 노트북·자동 생성 도구는 기본 구성에 넣지 않았습니다.
