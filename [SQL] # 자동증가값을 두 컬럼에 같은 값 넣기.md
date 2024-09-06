# [SQL] 자동증가값을 두 컬럼에 같은 값 넣기

권한이 있는 경우 : 시퀀스.nextval, 시퀸스.currval    
권한이 없는 경우 : 넣어야하는 구문 전체를 select Max() + 1 from DUAL

``` sql
INSERT INTO 테이블명 VALUES(SELECT * FROM dual)
INSERT INTO 테이블명 SELECT * FROM dual -- value 및 () 생략
```

```sql
INSERT INTO your_table (column1, column2, column3)
SELECT
  SubqueryAlias.new_value,
  SubqueryAlias.new_value,
  other_column
FROM another_table
```

```sql
INSERT INTO your_table (column1, column2, column3)
WITH SubqueryAlias AS (
  SELECT MAX(column1) + 1 AS new_value
  FROM your_table
  WHERE some_condition
)
SELECT
  SubqueryAlias.new_value,
  SubqueryAlias.new_value,
  other_column
FROM another_table
```


