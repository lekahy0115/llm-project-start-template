# 팀 환경 정보

팀원에게 공유할 **설정 결과**를 기입하는 문서입니다. 아래 `RENAME_ME_` 항목을 실제 값으로 바꿉니다.

| 항목 | 팀 공통 값 |
|---|---|
| GitHub Organization | `RENAME_ME_ORG` |
| GitHub Repository | `RENAME_ME_REPOSITORY` |
| GitHub URL | `https://github.com/RENAME_ME_ORG/RENAME_ME_REPOSITORY` |
| 기본 브랜치 | `main` |
| 공개 범위 | `Public` |
| GitHub Project Board 링크 | `RENAME_ME_PROJECT_BOARD_URL` |
| 개인별 Drive 상위 폴더 | `MyDrive/RENAME_ME_PROJECT/` |
| 개인 Git 저장소 폴더 | `MyDrive/RENAME_ME_PROJECT/repository/` |
| 공용 대용량 데이터 폴더 또는 바로가기 이름 | `MyDrive/RENAME_ME_SHARED_DATA/` |
| Drive 공동 사용 권한 | `RENAME_ME_ACCESS_POLICY` |
| 실험 결과 버전 기록 | `docs/DATA_MODEL_REGISTRY.md` |

**주의:** 팀 공용 폴더의 비공개 공유 URL이나 토큰·계정 정보는 Public GitHub에 올리지 마십시오. 필요한 접근 권한은 Google Drive의 계정별 공유 기능으로 부여합니다.

## 실행 환경 정보 (팀이 확정한 값만 기입)

| 항목 | 팀 공통 값 |
|---|---|
| 개발 환경 | Google Colab (`.ipynb`) |
| 노트북 실행 런타임 | `RENAME_ME_RUNTIME_CPU_OR_GPU` |
| Google Drive 마운트 경로 | `/content/drive/MyDrive/` |
| 개인별 Git 저장소 경로 | `/content/drive/MyDrive/RENAME_ME_PROJECT/repository/` |
| 공용 대용량 파일 경로 | `/content/drive/MyDrive/RENAME_ME_SHARED_DATA/` |
| 서비스용 노트북 경로 | `notebooks/service/RENAME_ME_SERVICE.ipynb` (서비스 제작 후) |
| 외부 시연 | ngrok (연결할 서버·포트는 서비스 구현 후 확정) |

공개 GitHub 문서에는 Google Drive **비공개 공유 링크, 계정 이메일, 토큰, ngrok 인증값**을 기록하지 않습니다. 공용 Drive 폴더의 실제 접근 권한은 관리자에게 별도 확인합니다.
