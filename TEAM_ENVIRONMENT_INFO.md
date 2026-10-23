# 팀 프로젝트 환경 정보

팀원들이 참고할 Repository·작업·저장 환경의 공통 정보입니다. `RENAME_ME_...` 항목은 실제 프로젝트 설정값이 입력되지 않은 상태를 뜻합니다.

## GitHub

| 항목 | 팀 공통 정보 |
|---|---|
| Organization | `RENAME_ME_ORGANIZATION` |
| Repository | `RENAME_ME_REPOSITORY` |
| Repository 주소 | `https://github.com/RENAME_ME_ORGANIZATION/RENAME_ME_REPOSITORY` |
| 공개 범위 | `RENAME_ME_VISIBILITY_PUBLIC_OR_PRIVATE` |
| 기본 브랜치 | `main` |
| 작업 브랜치 | `feature/작업명`, `fix/문제명` |
| 코드 통합 | 작업 브랜치 → Pull Request → 동료 검토 → `main` 병합 |
| 병합 방식 | `Squash and merge` 권장(저장소에서 허용된 경우) |
| GitHub Projects | `RENAME_ME_PROJECTS_LINK` |

## Google Colab

| 항목 | 팀 공통 정보 |
|---|---|
| 주 개발 파일 형식 | `.ipynb` |
| 시작 노트북 | `notebooks/00_COLAB_CONNECTION_CHECK.ipynb` |
| 기능 개발 위치 | `notebooks/development/` |
| 평가 위치 | `notebooks/evaluation/` |
| 서비스 시연 위치 | `notebooks/service/` |
| 실행 환경 | Google Colab 개인별 런타임(필요 시 GPU 사용) |
| GitHub 저장 | Colab의 `파일 → GitHub에 사본 저장`에서 **작업 브랜치** 확인 |

## Google Drive

| 항목 | 팀 공통 정보 |
|---|---|
| 공유 폴더 이름 | `RENAME_ME_SHARED_DRIVE_FOLDER` |
| 공유 폴더 링크 | `RENAME_ME_SHARED_DRIVE_LINK` (Private 저장소에서만 기입, Public이면 `별도 비공개 전달`) |
| Colab 기본 경로 | `/content/drive/MyDrive/RENAME_ME_SHARED_DRIVE_FOLDER` |
| 데이터 | `datasets/raw/`, `datasets/processed/` |
| 모델·체크포인트 | `models/`, `checkpoints/` |
| 결과물 | `outputs/` |

## 데이터 및 공개 범위

- GitHub: 노트북·설명 문서·공개 가능한 작은 예제 파일만 관리합니다.
- Google Drive: 원본 데이터, 모델 가중치, 학습 체크포인트, 대용량 결과물을 관리합니다.
- 개인정보, API 키, GitHub 액세스 토큰, ngrok 토큰은 GitHub 노트북·출력·문서에 기록하지 않습니다.
- Colab 런타임은 개인별 임시 실행 환경이며, 시연용 서비스는 상시 운영 환경이 아닙니다.
- Public 저장소에서는 비공개 Google Drive 공유 링크·팀원 이메일 등 내부 운영 정보를 공개 문서에 입력하지 않고 별도 채널로 전달합니다.

설정이 완료되기 전에는 위 `RENAME_ME_...` 주소와 이름을 실제 값으로 취급하지 않습니다.
