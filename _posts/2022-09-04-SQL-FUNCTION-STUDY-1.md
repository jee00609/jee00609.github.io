---
title: "SQL 공부 : COUNT, SUM, AVG, MIN, MAX"
categories:
  - SQL
tags: 
  - SQL
last_modified_at: 2022-09-04
---

취직을 하고 6개월이 조금 넘었다.

그동안 회사 업무에 적응하는 것이 바빠 포스팅을 하지 못했다.

회사에서 인프런 강의를 수강할 수 있도록 지원해주고 있다.

이걸 기회삼아 다시 부족한 실력을 차근차근 보수시켜 나갈 생각이다.

## COUNT

This function returns the number of items found in a group. 

이 함수는 그룹에서 찾은 항목의 수를 반환합니다.

COUNT always returns an int data type value.

COUNT 함수는 무조건 INT 형식의 데이터 타입으로 반환됩니다.

| ID | NAME | VISIT |
|----|------|-------|
| 1  | A    | 1     |
| 2  | A    | 2     |
| 3  | B    | 3     |
| 4  | C    | 5     |
| 5  | NULL | NULL  |

```sql
SELECT COUNT(*) FROM TEST;
-- RESULT : 5

SELECT COUNT(NAME) FROM TEST;
-- RESULT : 4

SELECT COUNT(DISTINCT NAME);
-- RESULT : 3 , DISTINCT 는 NULL 및 중복 제거
```


## SUM

Returns the sum of all the values, or only the DISTINCT values, in the expression. 

SUM can be used with numeric columns only. Null values are ignored.

식에서 모든 값의 합계 또는 DISTINCT 값만 반환합니다. 

SUM은 숫자 열에만 사용할 수 있습니다. Null 값은 무시됩니다.

```sql
-- Aggregate Function Syntax    
SUM ( [ ALL | DISTINCT ] expression )  

-- Analytic Function Syntax   
SUM ([ ALL ] expression) OVER ( [ partition_by_clause ] order_by_clause)

SELECT SUM(VISIT) FROM TEST;
-- RESULT : 11

SELECT AVG(VISIT) FROM TEST;
-- RESULT : 2.75 , NULL 값은 제외하여 분모가 4가 되어 계산된다.

SELECT SUM(VISIT)/COUNT(*) FROM TEST;
-- RESULT : 2.2 , COUNT(*) 를 통해 분모가 5가 되어 위의 값과 값이 달라진다. 
```


## AVG

This function returns the average of the values in a group. It ignores null values.

이 함수는 그룹에 있는 값의 평균을 반환합니다. null 값을 무시합니다.

```sql
AVG ( [ ALL | DISTINCT ] expression )  
   [ OVER ( [ partition_by_clause ] order_by_clause ) ]

SELECT AVG(VISIT) FROM TEST;
-- RESULT : 2.75 , NULL 값은 제외하여 분모가 4가 되어 계산된다.

SELECT SUM(VISIT)/COUNT(*) FROM TEST;
-- RESULT : 2.2 , COUNT(*) 를 통해 분모가 5가 되어 위의 값과 값이 달라진다. 
```


## MAX

Returns the maximum value in the expression.

표현식의 최대값을 반환합니다.

```sql
-- Aggregation Function Syntax  
MAX( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax  
MAX ([ ALL ] expression) OVER ( <partition_by_clause> [ <order_by_clause> ] ) 

SELECT MAX(VISIT) FROM TEST;
-- RESULT : 5 
```

## MIN

Returns the minimum value in the expression. 

May be followed by the <span style="color:blue"> [OVER clause](https://docs.microsoft.com/ko-kr/sql/t-sql/queries/select-over-clause-transact-sql?view=sql-server-ver16) </span> . 

표현식의 최소값을 반환합니다. 

[OVER 절](https://docs.microsoft.com/ko-kr/sql/t-sql/queries/select-over-clause-transact-sql?view=sql-server-ver16)이 뒤에 올 수 있습니다.

```sql
-- Aggregation Function Syntax  
MIN ( [ ALL | DISTINCT ] expression )  
  
-- Analytic Function Syntax   
MIN ( [ ALL ] expression ) OVER ( [ <partition_by_clause> ] [ <order_by_clause> ] )  

SELECT MIN(VISIT) FROM TEST;
-- RESULT : 1 
```

## 비고

3개월 안에 완강할 수 있도록 최소한 3일에 한번씩은 진도를 나갈 것 같다.

회사 업무도 열심히 하면서 공부 또한 열심히 하는 새나라의 어른이가 될 것이다...

개인적으로 [SW 개발자를 위한 성능 좋은 SQL 쿼리 작성법](https://www.inflearn.com/course/%EC%84%B1%EB%8A%A5%EC%A2%8B%EC%9D%80-%EC%BF%BC%EB%A6%AC%EC%9E%91%EC%84%B1%EB%B2%95)을 들어야 할 것 같다.

메모해두자

## 참고 사이트

[데이터 분석을 위한 중급 SQL](https://www.inflearn.com/course/%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B6%84%EC%84%9D-%EC%A4%91%EA%B8%89-sql)

[SQL 데이터베이스 함수](https://docs.microsoft.com/ko-kr/sql/t-sql/functions/functions?view=sql-server-ver16)