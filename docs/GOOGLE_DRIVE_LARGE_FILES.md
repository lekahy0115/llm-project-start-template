# Google Drive 대용량 데이터·모델 사용법

대용량 데이터셋, 원본·전처리 데이터, 모델 가중치, 체크포인트, 큰 실행 결과는 **Google Drive를 최종 저장·버전 관리 장소**로 사용합니다. 별도의 Git LFS나 Hugging Face 저장소를 필수로 요구하지 않습니다.

## 1. 하나의 공용 원본 폴더

폴더 소유자의 Drive에 `RENAME_ME_SHARED_DATA`를 하나 만들고 팀원에게 공유합니다. 팀원은 각자의 `내 드라이브`에 **동일한 이름의 바로가기**를 추가합니다.

```text
MyDrive/RENAME_ME_SHARED_DATA/
├── datasets/
│   ├── raw/v001/
│   └── processed/v001/
├── models/v001/
├── checkpoints/v001/
└── outputs/v001/
```

`v001`은 **버전 이름 예시**이며 실제 모델·데이터가 존재한다는 뜻이 아닙니다. 데이터나 가중치가 바뀌면 기존 파일을 덮어쓰지 않고 `v002/` 등의 새 폴더에 보관합니다.

## 2. 개인 Git 저장소와의 차이

- 개인 저장소: `/content/drive/MyDrive/RENAME_ME_PROJECT/repository/` — 코드·노트북·문서 Git 관리, 팀원마다 별도 복제본
- 공용 폴더: `/content/drive/MyDrive/RENAME_ME_SHARED_DATA/` — 대용량 파일 실제 저장, 팀원 모두 동일한 원본 접근

**공용 폴더 안에서 여러 명이 같은 Git 저장소를 동시에 관리하지 않습니다.**

## 3. 파일 읽기

서비스·평가 노트북에서 Drive 마운트 후 다음 경로를 사용합니다.

```python
from pathlib import Path
from google.colab import drive

drive.mount('/content/drive')
DATA_FILE = Path('/content/drive/MyDrive/RENAME_ME_SHARED_DATA/datasets/raw/v001/RENAME_ME_DATASET.csv')
print('파일 존재:', DATA_FILE.is_file())
# 실제 데이터 형식에 맞는 로딩 코드는 기능 개발 시 작성
```

파일 경로는 `DATA_MODEL_REGISTRY.md`의 등록 내용과 맞춰야 합니다. 많은 파일을 반복적으로 읽는 작업은 필요할 때 임시 디스크로 복사하여 사용할 수 있지만, 원본을 삭제하거나 Drive 파일 자체를 덮어쓰지 않습니다.

## 4. 모델 및 파인튜닝 가중치 저장

- 기본 모델은 사용 조건에 따라 공개 모델 제공처에서 불러오거나 Drive에 보관합니다.
- Full Fine-tuning 가중치든 LoRA 어댑터든 **실제 생성된 파일 크기에 따라** Drive의 버전 폴더에 저장합니다.
- 체크포인트는 실행·실험별 폴더로 구분합니다. 예: `checkpoints/v001/run_2026_01/`.
- GitHub에는 가중치 자체를 반드시 복사하지 않고, **어떤 코드 Commit과 어떤 Drive 버전이 연결되는지** 기록합니다.

## 5. Drive 버전 관리 규칙

Drive의 파일 버전 기록만으로 데이터셋·모델 실험 버전이 자동 관리되지는 않습니다. 팀에서 다음 기준을 직접 지킵니다.

1. 원본 파일은 덮어쓰지 않음
2. 변경 시 새 버전 폴더 `v002/`, `v003/` 생성
3. 저장 경로·크기·SHA-256(가능하면)·사용 모델·학습/전처리 조건을 `DATA_MODEL_REGISTRY.md`에 기록
4. 해당 파일을 사용한 Git Commit 해시와 평가 결과를 연결
5. 공용 폴더에서 다른 팀원의 파일을 임의로 삭제·이동하지 않음

## 6. Public Repository와 접근 권한

Google Drive 공용 원본 폴더는 팀원 계정에게만 공유해도 됩니다. 다만 외부 면접관은 별도 권한이 없으면 파일을 내려받을 수 없습니다. 따라서 공개 가능한 샘플 데이터·모델 출처·버전·실행 방법을 README와 등록표에 남기고, 재현 가능한 범위와 접근 제한을 명확히 적습니다.

참고: https://support.google.com/drive/answer/9700156 · https://research.google.com/colaboratory/faq.html
