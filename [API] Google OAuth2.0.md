



# 1. authorization code 얻기

# 2. access token 얻기 with authorization code

1번에서 얻은 authorization code값으로 액세스토큰 얻기
<br>

이전에는 OAuth 2.0이라고 해도 서비스 계정 타입으로 만들었으나, 이번에는 OAuth 클라이언트ID방식으로 진행
서비스 계정 생성에서 클라이언트ID방식 선택하고 클라이언트ID, 클라이언 pw(client secrets) 값을 받아옴

<br><br>


## 1) authorization code 얻기

인증요청 코드 
```java
https://accounts.google.com/o/oauth2/auth
?response_type=code
&redirect_uri=http://localhost/index.do&scope=https://www.googleapis.com/auth/analytics
&client_id=72207699-t3vsgfeak2ljk0o7130thhij.apps.googleusercontent.com
```

**Google API의 OAuth 2.0 범위(Scope지정 관련) 참고 자료**
https://developers.google.com/identity/protocols/oauth2/scopes?hl=ko

```java
// example
https://accounts.google.com/o/oauth2/auth?response_type=code&redirect_uri=http://localhost/index.do&scope=https://www.googleapis.com/auth/analytics&client_id=722057675499-t3vsgfeak2bufu90thhij.apps.googleusercontent.com
```

인증 후 redirection 받은 url
code부분이 authorization code값
```java
http://localhost/index.do
?code=**4/0AeaYSpJzV9-PoD75tQubf5iALDOQf-c_Ds9lPjItPFN0fw-2w**
&scope=https://www.googleapis.com/auth/analytics
```
<br><br>

## 2) access token 얻기

```java
https://oauth2.googleapis.com/token
?code=authorization code
&clientid=클라이언트아이디
&clientsecret=클라이언트시크릿
&redirect_uri=https://localhost:8080/auth/google/callback
&grant_type=authorization_code
```
```java
// example
https://oauth2.googleapis.com/token
?code=4/0AeaYSp55Q-8FT-yfhDdK-d1XfMihiruNJ5iO8hNmn3hqfAb_i1U3g
&client_id=7220575499-t3vsgfea0o71351hbuthhij.apps.googleusercontent.com
&client_secret=GOPX-REQG-7u1yMeGC36m8GPV
&redirect_uri=http://localhost/index.do
&grant_type=authorization_code
```
<br>


response 받은 access token
```java
{
  "access_token": "ya9.a0Ad52N37EQ6P3vl-oaKEz3yGVZ7W2clhIL6fUDTRvxCshz4RQk-0l4ZMPy0kx_HI4uTbGpMcmGx_5FOVq_3Apnfu04WcGYdVbTPQYZqhX6_MGFnlANRIA8vbxzJ1115vgyLrtOdcVJJ69hC5fPqClaCYASARMSFQHGX2MifIGiL4y_lccO4vI8y-Q0171",
  "expires_in": 3599,
  "scope": "https://www.googleapis.com/auth/analytics",
  "token_type": "Bearer"
}
```