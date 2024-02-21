# 리눅스(Linux) 전역변수 영구설정 방법 2가지

## 방법1./etc/profile

```bash
vi /etc/profile   # profile 파일로 진입
# 대문자 G키(Shift + G)로 최하단으로 이동

export GOOGLE_APPLICATION_CREDENTIALS=/etc/google_auth/파일명

source google_credentials.sh    # source : 적용 명령어
$GOOGLE_APPLICATION_CREDENTIALS # 등록한 전역변수 호출

# 호출 결과
/etc/google_auth/파일명
```

## 방법2./etc/profile.d내에 sh파일로 생성
방법1 /etc/**profile**의 경우, OS를 업데이트 시에 파일이 변경될 가능성 있음 
1. 보완책1 : 파일 백업
1. 보완책2 : /etc/profile.d 경로에 sh파일로 생성


```bash
cd /etc/profile.d/           # 해당 경로로 이동
touch google_credentials.sh  # sh파일 생성
vi google_credentials.sh     # 만든 파일로 진입

# export 환경 변수명=경로
ex) 
export GOOGLE_APPLICATION_CREDENTIALS=/etc/google_auth/파일명

source google_credentials.sh    # source : 적용 명령어
$GOOGLE_APPLICATION_CREDENTIALS # 등록한 전역변수 호출

# 호출 결과
/etc/google_auth/파일명
```
