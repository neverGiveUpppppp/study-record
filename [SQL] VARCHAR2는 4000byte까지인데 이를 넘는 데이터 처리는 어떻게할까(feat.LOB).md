# [SQL] varchar2는 4000byte까지인데 이를 넘는 데이터 처리는 어떻게할까? (feat.LOB)


대용량 처리 자료형 : LOB    
대용량 문자처리 자료형 : CLOB     
&nbsp;&nbsp;&nbsp;&nbsp;(char의 C + LOB)     



<br><br>

## CLOB의 필요성
varchar2는 최대 4000byte이기 때문에 4000byte가 넘는 고용량들을 다룰 때, clob이 필요

<br><br>

## 문제점
CLOB을 그냥 쓰면 자바 객체 출력 때처럼 객체주소가 찍혀 나오는 것처럼 출력됨

<br><br>

## 해결책
DBMS_LOB.SUBSTR() 사용

```sql
DBMS_LOB.SUBSTR(CLOB컬럼명, 자를 문자 수, 시작위치offset) // (적용할 컬럼명, 몇개를 가져올 지, 시작위치)
```
<br><br>

### 주의사항
#### 1)TO_CLOB()으로 감싸기
TO_CLOB(클롭컬럼명)으로 감싸지 않으면, 식별자가 너무 길다는 오류 발생 가능성

```sql
TO_CLOB(CONTENT)
```

#### 2)길이 한도

CLOB 자체는 4000넘어도 되지만 DBMS_LOB.SUBSTR()을 쓰면 4000까지만 가능

따라서, 4000이 넘는 CLOB데이터를 조회할 때는 이어 붙이고 alias로 하나로 가져가면 됨

||이나 concat() 사용

ex) 1-4000 + 4001-8000 식으로 문자열 이어 붙이는 방법

```sql
DBMS_LOB.SUBSTR(col1, 4000, 1) || DBMS_LOB.SUBSTR(col1, 4000, 4001) AS CONTENTS 
```

```sql
SELECT 
		TITLE, 
		WRTIER,
		DBMS_LOB.SUBSTR(col1, 4000, 1) || DBMS_LOB.SUBSTR(col1, 4000, 4001) AS **CONTENTS**
FROM BOARD

```
<br><br><br>

### 관련 함수
```sql
DBMS_LOB.INSTR(CLOB컬럼명, '검색할 단어', 몇번째 위치한 단어)  // 찾으려는 문자열의 인덱스번호 반환
DBMS_LOB.GETLENGTH(CLOB컬럼명)                         // 해당 컬럼의 길이 반환
```

#### 1)DBMS_LOB.INSTR()

지정한 문자열이 나올 때마다 해당 인덱스 번호 반환

LIKE보다 조회 빠름

#### 2)DBMS_LOB.GETLENGTH()

해당 컬럼의 전체 길이 반환(공백 포함)
<br><br>


참고자료    
https://developyo.tistory.com/364
https://joongwoonc.tistory.com/52


