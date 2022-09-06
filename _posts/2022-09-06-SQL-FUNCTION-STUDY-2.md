---
title: "SQL 공부 : GROUP BY , HAVING"
categories:
  - SQL
tags: 
  - SQL
last_modified_at: 2022-09-06
---

현재 회사에서 구현하고 있는 검수 관리라는 업무에 대한 프로세스를 이해할수록 기분이 좋아진다.

회사 업무가 SAP SCM (공급망 관리) 쪽이다보니 각 테이블들간의 관계, 연결고리를 이해하고 쿼리를 짜는 기술이 필요했다.

코딩하는 실력이나 업무를 이해하는 능력이 다른 팀원들에 비해 부족하다고 느끼고 있어서 더욱 공부를 해야한다고 느낀다...

## 테이블

| ProductID | ProductName                  | SupplierID | CategoryID | Unit                | Price |
|-----------|------------------------------|------------|------------|---------------------|-------|
| 1         | Chais                        | 1          | 1          | 10 boxes x 20 bags  | 18    |
| 2         | Chang                        | 1          | 1          | 24 - 12 oz bottles  | 19    |
| 3         | Aniseed Syrup                | 1          | 2          | 12 - 550 ml bottles | 10    |
| 4         | Chef Anton's Cajun Seasoning | 2          | 2          | 48 - 6 oz jars      | 22    |
| 5         | Chef Anton's Gumbo Mix       | 2          | 2          | 36 boxes            | 21.35 |
| 6         | Grandma's Boysenberry Spread | 3          | 2          | 12 - 8 oz jars      | 25    |

## GROUP BY

> A SELECT statement clause that divides the query result into groups of rows, usually for the purpose of performing one or more aggregations on each group. <br/>
> The SELECT statement returns one row per group.

> 일반적으로 각 그룹에 대해 하나 이상의 집계를 수행하기 위해 쿼리 결과를 행 그룹으로 나누는 SELECT 문 절입니다. <br/>
> SELECT 문은 그룹당 하나의 행을 반환합니다.

GROUP BY 조건으로 적혀있는 컬럼을 SELECT 문에 추가해서 결과를 볼 수 있다.

   * 사용법

```sql
-- Syntax for SQL Server and Azure SQL Database   
-- ISO-Compliant Syntax  
  
GROUP BY {
      column-expression  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
    | GROUPING SETS ( <grouping_set> [ ,...n ]  )  
    | () --calculates the grand total 
} [ ,...n ] 
```

   * 기본 쿼리

```sql
SELECT 	  SupplierID
       	 , ProductName
	 , AVG(Price)
FROM Products
GROUP BY SupplierID;
```

   * 결과

| 1 | Chais                        | 15.666666666666666 |
|---|------------------------------|--------------------|
| 2 | Chef Anton's Cajun Seasoning | 20.35              |
| 3 | Grandma's Boysenberry Spread | 31.666666666666668 |
| 4 | Mishi Kobe Niku              | 46                 |
| 5 | Queso Cabrales               | 29.5               |
| 6 | Konbu                        | 14.916666666666666 |

   * 조건절 추가 쿼리

```sql
SELECT 	  SupplierID
       	 , CategoryID
       	 , ProductName
	 , AVG(Price)
FROM Products
GROUP BY SupplierID
	 ,CategoryID;
```

   * 결과

| SupplierID | CategoryID | ProductName                     | AVG(Price) |
|------------|------------|---------------------------------|------------|
| 1          | 1          | Chais                           | 18.5       |
| 1          | 2          | Aniseed Syrup                   | 10         |
| 2          | 2          | Chef Anton's Cajun Seasoning    | 20.35      |
| 3          | 2          | Grandma's Boysenberry Spread    | 32.5       |
| 3          | 7          | Uncle Bob's Organic Dried Pears | 30         |
| 4          | 6          | Mishi Kobe Niku                 | 97         |
| 4          | 7          | Longlife Tofu                   | 10         |
| 4          | 8          | Ikura                           | 31         |
| 5          | 4          | Queso Cabrales                  | 29.5       |
| 6          | 2          | Genen Shouyu                    | 15.5       |
| 6          | 7          | Tofu                            | 23.25      |
| 6          | 8          | Konbu                           | 6          |


   * TIP
      * MYSQL 의 경우 GROUP BY 조건절에 숫자를 지원한다.
      * SELECT 에 있는 N번째 컬럼으로 조건을 걸고 싶을 경우 GROUP BY N; 으로 작성할 수 있다. 
      * 그러나 <span style="color:red">비가시적</span>이기 때문에 <span style="color:red">지양하</span>는 것이 좋다.

   * ORDER BY 구문 추가 쿼리

```sql
SELECT 	  SupplierID
       	 , CategoryID
       	 , ProductName
	 , AVG(Price)
FROM Products
GROUP BY SupplierID
	 ,CategoryID
ORDER BY AVG(Price) DESC;
```

   * 결과

| SupplierID | CategoryID | ProductName                     | AVG(Price) |
|------------|------------|---------------------------------|------------|
| 4          | 6          | Mishi Kobe Niku                 | 97         |
| 3          | 2          | Grandma's Boysenberry Spread    | 32.5       |
| 4          | 8          | Ikura                           | 31         |
| 3          | 7          | Uncle Bob's Organic Dried Pears | 30         |
| 5          | 4          | Queso Cabrales                  | 29.5       |
| 6          | 7          | Tofu                            | 23.25      |
| 2          | 2          | Chef Anton's Cajun Seasoning    | 20.35      |
| 1          | 1          | Chais                           | 18.5       |
| 6          | 2          | Genen Shouyu                    | 15.5       |
| 1          | 2          | Aniseed Syrup                   | 10         |
| 4          | 7          | Longlife Tofu                   | 10         |
| 6          | 8          | Konbu                           | 6          | 

## HAVING

> Specifies a search condition for a group or an aggregate. <br/>
> HAVING can be used only with the SELECT statement. <br/>
> HAVING is typically used with a GROUP BY clause. <br/>
> When GROUP BY is not used, there is an implicit single, aggregated group.<br/>

> 그룹 또는 집계에 대한 검색 조건을 지정합니다. <br/>
> HAVING은 SELECT 문에서만 사용할 수 있습니다. <br/>
> HAVING은 일반적으로 GROUP BY 절과 함께 사용됩니다. <br/>
> GROUP BY가 사용되지 않으면 암시적인 단일 집계 그룹을 사용합니다.<br/>

   * TIP
      * SQL 순서에서 WHERE 절은 GROUP BY 보다 순서 상 우선순위에 있다.
      * GROUP BY 를 적용한 결과 값에 대해 조건을 추가하고자 할 때 HAVING 을 사용한다.

   * 사용법

```sql
[ HAVING <search condition> ]  
HAVING AVG(Price) >= 10;
```

   * 예제 쿼리

```sql
/*잘못된 쿼리*/
SELECT 	  SupplierID
       	 , CategoryID
       	 , ProductName
	 , AVG(Price)
FROM Products
WHERE AVG(Price) >= 10
GROUP BY SupplierID
	 ,CategoryID;

/*HAVING 을 사용해서 조건을 적용*/
SELECT 	  SupplierID
       	 , CategoryID
       	 , ProductName
	 , AVG(Price)
FROM Products
GROUP BY SupplierID
	 ,CategoryID
HAVING AVG(Price) >= 10;
```

   * 결과

| SupplierID | CategoryID | ProductName                     | AVG(Price) |
|------------|------------|---------------------------------|------------|
| 1          | 1          | Chais                           | 18.5       |
| 1          | 2          | Aniseed Syrup                   | 10         |
| 2          | 2          | Chef Anton's Cajun Seasoning    | 20.35      |
| 3          | 2          | Grandma's Boysenberry Spread    | 32.5       |
| 3          | 7          | Uncle Bob's Organic Dried Pears | 30         |
| 4          | 6          | Mishi Kobe Niku                 | 97         |
| 4          | 7          | Longlife Tofu                   | 10         |
| 4          | 8          | Ikura                           | 31         |
| 5          | 4          | Queso Cabrales                  | 29.5       |
| 6          | 2          | Genen Shouyu                    | 15.5       |
| 6          | 7          | Tofu                            | 23.25      |
| 6          | 8          | Konbu                           | 6          |


## 참고 사이트

[데이터 분석을 위한 중급 SQL](https://www.inflearn.com/course/%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B6%84%EC%84%9D-%EC%A4%91%EA%B8%89-sql)

[SELECT - GROUP BY- Transact-SQL](https://docs.microsoft.com/ko-kr/sql/t-sql/queries/select-group-by-transact-sql?view=sql-server-ver16)

[SELECT - HAVING (Transact-SQL)](https://docs.microsoft.com/ko-kr/sql/t-sql/queries/select-having-transact-sql?view=sql-server-ver16)