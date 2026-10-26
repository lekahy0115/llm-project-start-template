# ngrok을 이용한 웹 서비스 시연

서비스 개발이 완료된 후, `notebooks/service/RENAME_ME_SERVICE.ipynb` 파일에서 **웹 서버를 실행**하고 그 서버 포트를 **ngrok HTTP 터널**에 연결합니다. 노트북 파일명과 서버 프레임워크는 프로젝트가 결정되면 정합니다.

## 1. 서비스 노트북 준비

경로 예시:

```text
/content/drive/MyDrive/RENAME_ME_PROJECT/repository/notebooks/service/RENAME_ME_SERVICE.ipynb
```

이 파일에서 필요한 데이터·모델을 `/content/drive/MyDrive/RENAME_ME_SHARED_DATA/`에서 불러옵니다. 서비스용 코드와 UI는 프로젝트 개발 시 작성합니다.

## 2. 서버 포트 확인

예를 들어 서비스가 로컬 포트 `7860`에 실행된다면 `http://127.0.0.1:7860`으로 내부 접속할 수 있어야 합니다. 다른 프레임워크를 사용할 경우 **실제 서버 포트**로 변경합니다.

Gradio를 선택한 경우 `share=True`를 사용할 필요는 없습니다. ngrok으로 접근할 것이므로 내부 서버를 시작하는 설정을 사용합니다.

## 3. ngrok 연결 예시

서비스 노트북의 **서버 시작 셀 다음 셀**에서 다음을 실행할 수 있습니다.

```python
%pip -q install pyngrok

from getpass import getpass
from pyngrok import ngrok

NGROK_TOKEN = getpass('ngrok authtoken: ')
ngrok.set_auth_token(NGROK_TOKEN)

# 7860은 예시입니다. 앞 셀에서 실제 실행한 서버 포트로 변경합니다.
tunnel = ngrok.connect(7860, "http")
print('시연 URL:', tunnel.public_url)
```

`getpass`는 토큰을 화면에 출력하지 않고 입력받기 위한 방법입니다. 토큰을 노트북 파일에 하드코딩하거나 GitHub에 Commit하지 않습니다.

## 4. 시연·종료

1. 출력된 HTTPS URL을 별도 브라우저에서 열어 화면 확인
2. 모델 입력→응답까지 전체 동작 확인
3. 시연이 끝나면 서비스 서버와 터널 종료 (`ngrok.disconnect(tunnel.public_url)` 가능)

런타임이 종료되면 시연 서버와 터널도 중단됩니다. 이것은 상시 운영 호스팅이 아니라 프로젝트 웹 시연 방식입니다.

참고: https://pyngrok.readthedocs.io/en/latest/integrations.html · https://ngrok.com/docs

## 시연 실행 순서와 확인 사항

1. **개인 Drive의 Git 저장소** `notebooks/service/RENAME_ME_SERVICE.ipynb`를 엽니다. 해당 파일은 실제 서비스를 개발한 뒤 생성합니다.
2. 서비스 노트북에서 **공용 Drive의** `RENAME_ME_SHARED_DATA`에 있는 승인된 모델·데이터 버전을 불러옵니다. 데이터 버전과 실제 Git Commit은 `DATA_MODEL_REGISTRY.md`에 연결해 둡니다.
3. 노트북에서 선택한 웹 UI 또는 API 서버를 `127.0.0.1`의 정해진 포트로 시작합니다.
4. 같은 런타임에서 ngrok 인증을 진행하고 **그 서버 포트로** HTTP 터널을 연결합니다. ngrok 인증 토큰은 공개 노트북이나 GitHub에 기록하지 않습니다.
5. 반환된 외부 URL을 **별도 브라우저**에서 열어 입력 → 추론 → 결과 표시가 작동하는지 확인합니다.
6. 시연 종료 시 터널과 서버를 종료합니다. 런타임 종료 시 시연 링크가 더 이상 동작하지 않을 수 있습니다.

서비스 방식과 포트가 아직 결정되지 않았으므로 이 문서는 특정 서버 코드를 미리 구현하지 않습니다. **ngrok만으로 웹 UI가 만들어지지는 않으며**, 실행 중인 웹 서버가 있어야 접속할 수 있습니다.

## 역할 구분
- GitHub: 서비스 노트북, 변경 기록, 사용 방법, 평가 결과
- 개인 Google Drive: Git 저장소 복제본과 노트북 저장
- 공용 Google Drive: 큰 모델·데이터 및 버전별 결과
- Colab 런타임: 실행 중인 웹 서버·모델 추론
- ngrok: 그 서버 포트의 외부 접속 주소 제공
