# 프로젝트 폴더 및 파일 구조

## 1. 전체 구성

```text
RENAME_ME_PROJECT_NAME/                  ← 프로젝트에 맞게 이름 변경
├── .github/
│   └── README.md                       ← GitHub 관련 설정 파일 위치 안내
├── notebooks/                           ← Colab 노트북 중심 개발
│   ├── README.md
│   ├── 00_COLAB_CONNECTION_CHECK.ipynb  ← Drive·런타임 연결 확인
│   ├── development/
│   │   └── .gitkeep
│   ├── evaluation/
│   │   └── .gitkeep
│   └── service/
│       └── .gitkeep
├── data/
│   ├── README.md
│   └── samples/
│       └── .gitkeep                    ← GitHub 공유용 작은 예제
├── configs/
│   └── README.md                       ← 기술 확정 후 설정 파일 보관
├── assets/
│   └── README.md                       ← 이미지·화면 자료
├── outputs/
│   └── README.md                       ← 임시/로컬 출력; Git 추적 제외
├── docs/
│   ├── TEAM_ENVIRONMENT_INFO.md         ← 팀에 공유할 설정 결과/주소
│   ├── TEAM_COMMON_SETUP.md            ← 모든 팀원이 할 최초 연결 설정
│   ├── TEAM_COLLABORATION_WORKFLOW.md   ← 브랜치·Colab 저장·PR·병합
│   └── SERVICE_DEMO.md                 ← Colab 서비스 시연 흐름
├── .gitignore                          ← 인증정보·체크포인트 등 제외 규칙
├── README.md                           ← 프로젝트 안내 및 문서 바로가기
└── STRUCTURE.md                        ← 지금 읽는 설명 문서
```

`development/`, `evaluation/`, `service/` 안의 `.gitkeep`은 빈 폴더를 GitHub에도 표시하기 위한 파일이며 실행되지 않습니다.

## 2. 각 폴더의 목적과 사용 예시

### `notebooks/` — Colab에서 직접 여는 주 개발 파일

- `00_COLAB_CONNECTION_CHECK.ipynb`: Colab 런타임 및 공유 Google Drive 경로를 확인합니다.
- `development/`: 기능 구현·수정·실험용 노트북을 놓습니다. 예: `RENAME_ME_document_summary.ipynb`.
- `evaluation/`: 정확도/응답 시간 등 평가용 노트북을 놓습니다. 예: `RENAME_ME_response_evaluation.ipynb`.
- `service/`: 시연용 웹 UI·추론 요청 처리를 **노트북에서 실행**할 때 사용합니다. 예: `RENAME_ME_service_demo.ipynb`.

이름에 `RENAME_ME_`가 붙은 예시 파일은 **아직 생성되지 않았으며**, 실제 담당 기능에 맞게 새로 만듭니다. 각 파일을 여러 사람이 동시에 수정하면 `.ipynb` 병합 충돌이 어려우므로 담당 노트북을 분리합니다.

### `data/samples/` — GitHub로 공유하는 소규모 예제

예: 개인정보가 제거된 `example_input.json`이나 공개 허용된 5행짜리 `example.csv`. 여기 넣은 파일은 기본적으로 Git 추적 대상입니다. 민감정보·원본 대량 데이터는 이 폴더에 두지 않습니다.

### `configs/` — 설정을 코드에서 분리할 때

예: 기술 선정 후 추가할 `RENAME_ME_model_settings.json` 같은 **비밀정보 없는** 설정 파일. 특정 LLM·RAG·프레임워크는 미리 지정하지 않습니다. API 키, 토큰 및 비밀번호는 설정 파일에 기록하지 않습니다.

### `assets/` — 설명 및 서비스 자료

예: 서비스 화면 설명 그림(`ui_flow.png`), 로고 또는 발표용 공개 이미지. 모델 가중치나 데이터셋 보관 장소가 아닙니다.

### `outputs/` — 런타임 생성물의 임시 위치

예: 실험 중 만들어진 임시 텍스트·로그·그림. `outputs/` 아래 생성물은 `.gitignore`로 Git 추적에서 제외합니다. 여러 사람이 공유하거나 오래 보관할 결과는 Google Drive의 `outputs/`에 저장합니다.

### `docs/` — 팀원이 직접 읽을 운영·사용 문서

- `TEAM_ENVIRONMENT_INFO.md`: 실제 Repository/Drive 주소와 팀의 합의된 운영 정책을 확인하는 결과 문서입니다. 미확정 항목은 `RENAME_ME_...`로 표시했습니다.
- `TEAM_COMMON_SETUP.md`: 각 팀원이 자신의 GitHub·Google 계정으로 설정하는 절차입니다.
- `TEAM_COLLABORATION_WORKFLOW.md`: 작업 브랜치 생성부터 Colab 저장, PR 검토·병합·다음 작업까지의 순서입니다.
- `SERVICE_DEMO.md`: Colab에서 서비스 시연을 실행할 때 필요한 구성과 제한 사항입니다.

### `.github/` — GitHub 저장소 구성 관련 위치

현재는 용도 안내만 들어 있습니다. GitHub Issues, Projects, PR, 브랜치 보호 설정은 GitHub 웹 화면에서 관리할 수 있으므로 별도의 자동화·이슈·PR 템플릿은 만들지 않았습니다.

## 3. 이름 변경이 가능한 항목과 고정 권장 항목

| 항목 | 변경 기준 | 예시 |
|---|---|---|
| ZIP 최상위 `RENAME_ME_PROJECT_NAME` | 실제 프로젝트명으로 변경 | `news-verification-demo` |
| GitHub Organization·Repository명 | 소유자가 정하는 실제 계정/프로젝트명 | `YOUR_ORG/YOUR_REPO` |
| Google Drive 공유 루트 `RENAME_ME_SHARED_DRIVE_FOLDER` | 관리자와 팀원이 같은 이름 사용 | `news-verification-data` |
| `RENAME_ME_...ipynb` | 담당 기능에 맞게 파일명 선택 | `document_summary.ipynb` |
| `RENAME_ME_...json` | 사용하는 설정 내용에 맞게 파일명 선택 | `model_settings.json` |
| `README.md`, `STRUCTURE.md`, `docs/*.md` | 문서 링크의 안정성을 위해 가급적 유지 | 변경 시 연결된 링크도 수정 |
| `notebooks/`, `data/`, `configs/`, `assets/`, `outputs/`, `docs/` | 공통 경로이므로 가급적 유지 | 변경 시 문서·Colab 경로도 수정 |

`RENAME_ME_...`는 변수명 표기용이며 실제 값이 아닙니다. 예시를 자신의 실제 프로젝트 정보로 바꾸기 전에는 해당 경로가 작동하지 않습니다.

## 4. Google Drive에서 따로 만드는 저장 구조

다음은 **GitHub ZIP에 포함된 폴더가 아니라**, 소유자가 Google Drive에 만들고 팀원에게 공유하는 폴더입니다.

```text
My Drive/
└── RENAME_ME_SHARED_DRIVE_FOLDER/         ← 실제 공유 폴더명
    ├── datasets/
    │   ├── raw/                         ← 원본 데이터
    │   └── processed/                   ← 전처리 결과
    ├── models/                          ← 모델 가중치
    ├── checkpoints/                     ← 중간 학습 상태
    └── outputs/                         ← 공유/보존할 결과
```

Colab에서는 팀원 각자의 Google Drive를 `/content/drive`에 마운트합니다. 공유 폴더는 각자의 `내 드라이브` 최상위에 **같은 이름의 바로가기**를 만들어 접근하도록 맞춥니다.

## 5. Colab 기반 개발부터 시연까지

1. 팀원은 자신의 **작업 브랜치**에서 해당 `.ipynb`를 Colab으로 엽니다.
2. Colab 런타임에서 Google Drive를 연결하고 필요한 데이터·모델을 읽습니다.
3. `notebooks/development/` 등에서 기능을 구현합니다. 검증할 코드는 `evaluation/`의 별도 노트북에 둘 수 있습니다.
4. 노트북은 **GitHub 작업 브랜치에 명시적으로 저장**하고 PR을 만듭니다. Colab의 일반 저장만으로 GitHub에 Commit되는 것은 아닙니다.
5. 팀원이 PR을 검토하고 `main`에 병합합니다.
6. 최종 시연 시 `notebooks/service/`에서 서비스 노트북을 열고 사용자 입력 → 모델 추론 → 결과 표시 흐름을 실행합니다. 웹 UI와 외부 접근 터널은 실제 기술을 정한 뒤 노트북에서 구성합니다.

Colab 런타임은 영구 서버가 아닙니다. 시연 서비스는 런타임이 종료되면 중단될 수 있습니다.

## 6. `.py` 서비스로 확장할 수 있나요?

가능합니다. 기능이 커지면 그때 `src/` 또는 `app/` 폴더를 추가해 노트북의 데이터 처리·추론·서버 로직을 `.py` 파일로 옮기면 됩니다. 현재는 이 구조가 불필요하므로 만들지 않았습니다. 기존 GitHub 브랜치·PR·Drive 데이터 관리 방식은 계속 활용할 수 있습니다.
