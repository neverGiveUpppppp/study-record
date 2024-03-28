

# MERGE INTO(=ON DUPLICATE KEY UPDATE)
<br>
기존 데이터는 UPDATE하고 신규 데이터는 INSERT하는 기능

<br>

| DataBase | Query |
| --- | --- |
| MySQL | ON DUPLICATE KEY UPDATE |
| Oracle | MERGE INTO |
| MSSQL | IN NOT EXISTS |

**MERGE INTO = ON DUPLICATE KEY UPDATE = IN NOT EXISTS**
<br><br><br>



## [Oracle] MERGE INTO

MERGE 에서의 DELETE 구문은 DELETE 단독 구문이 아닌 UPDATE 구문에 종속됨    
UPDATE 실행된 건에 한해서 DELETE 구문이 수행된다
<br><br>

### MERGE INTO

하나의 쿼리문으로 INSERT, UPDATE, DELETE 작업을 해야 하는 경우,    
이럴 때에는 MERGE 문을 사용하면 간단하게 쿼리문을 작성

```sql
MERGE INTO 테이블/뷰
    USING 테이블/뷰/듀얼
        ON 조건 - UPDATE와 INSERT를 처리할 조건문                
    WHEN MATCHED THEN
        UPDATE SET 컬럼1 = 밸류,
                    컬럼2 = 밸류,
                    ...
        DELETE 테이블 WHERE 컬럼1 = 밸류   -- DELETE문 생략가능
                        AND 컬럼2 = 밸류 ...
    WHEN NOT MATCHED THEN
            INSERT(컬럼1,컬럼2,컬럼3,...) VALUES(밸류값1,밸류값2, ...)						 
			
```
<br><br>


## [MySql] **ON DUPLICATE KEY UPDATE**

Primary Key 또는 Unique Index를 기준점으로    
insert 하려는 데이터가 해당 컬럼의 내용과 중복되는 경우, 
기존 데이터를 delete하고 새 데이터는 insert하는 문법

```sql
INSERT INTO 테이블명 VALUES(컬럼명1,컬럼명2...)
	ON DUPLICATE KEY UPDATE 키를 제외한 컬럼명 = 밸류값 ...
```
<br>

#### ※ ON DUPLICATE KEY UPDATE 작동방식

1.INSERT 문을 실행하여 신규 데이터를 입력    
2.UNIQUE KEY( name컬럼 )의 에 중복되는 값을 확인    
3.중복된 UNIQUE KEY값이 존재하면, ON DUPLICATE KEY UPDATE 지정된 컬럼을 UPDATE    
4.마지막으로 새로 INSERT된 중복되는 UNIQUE KEY값을 가진 항목을 DELETE    

<br><br>


참고자료    
https://210one2.tistory.com/393    
https://wickedmagica.tistory.com/253    
https://dkswnkk.tistory.com/543    
https://kkangdda.tistory.com/53    