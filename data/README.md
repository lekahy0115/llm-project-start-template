# 데이터 보관 규칙

- `samples/`: GitHub에서 팀원들이 공유해도 되는 작은 예제 데이터만 둡니다.
- 원본 데이터·대용량 데이터·개인정보 포함 자료: Google Drive의 `datasets/raw/` 등 공유 저장소에 둡니다.
- 전처리 결과: Google Drive의 `datasets/processed/`에 둡니다.

예: `samples/example_input.json`은 작은 공개 가능 예제라면 Commit할 수 있습니다. `samples/` 폴더에 대한 전체 제외 규칙은 `.gitignore`에 없습니다. API 키·개인정보가 들어간 파일은 크기가 작더라도 절대로 Commit하지 않습니다.
