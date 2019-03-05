# Toonie API
투니서버와 투니 앱클라이언트 사이에 쓰이는 API
RESTFull API로, JSON 형식으로 데이터를 주고 받는다.

## API list
1. App Vesion API
2. Token API
3. Keyword API
4. Keyword And Tag API
5. Tag And Toon API
6. BookMark API

### App Version API
APP 버전 정보를 조회하는 API로 GET METHOD만 지원하고, 이 API를 호출함으로서, 업데이트되어야 하는 Vesion 정보를 확인 할 수 있다.

#### GET : /appVersion

#### Request
```
    Null(보내지 않음)
```

#### Response
|KEY|VALUE|
|---
|succces|API 호출 성공 여부|
|foreUpdateYn|강제 업데이트 여부|
|limitVersion|업데이트가 필요한 버전정보(이 버전 이하로는 업데이트 필요|
|updateMessage|업데이트 메세지|
|updateRedirectURL|업데이트 Redirect URL|

```
    {
        "success" : "success",
        "foreUpdateYn" : "Y",
        "limitVersion" : "1.0.0",
        "updateMessage" : "현재 사용할 수 없는 버전입니다."
        "updateRedirectURL" : "www.itunes.com/istore/.."
    }
```