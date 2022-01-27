---
title: "[Oracle] 오라클 기본함수 : 날짜함수, 변환함수"

categories:
  - oracle
tags: 
  - DBMS
  - SQL
  - Oracle

last_modified_at: 2022-01-28
---

날짜함수와 변환함수를 배워 보았다.

IF ELSE 문은 어디서 쓰이는거지?

MySQL 로 사용할 땐, Java 단에서 해결했던 걸로 기억하는데, 따로 사용되는 곳이 있는 것 같다.

알아두면 언젠간 쓸 수 있는게 공부니깐 군말없이 정리하고자 한다.

오늘 실습한 문자함수
   * sysdate
   * months_between
   * add_months
   * next_day
   * last_day
   * to_char
   * nvl
   * decode
   * case


```sql
-- sysdate -> 날짜 를 출력
-- 출력 : 27-JAN-22
select sysdate from dual;

-- months_between
-- 31일 이후부터 오늘 날짜와의 개월 수를 구한 것
-- 출력 : 1
select months_between(sysdate+31,sysdate) from dual;

-- add_months
-- 현재 날짜에서 7 개월을 더함
-- 출력 : 27-AUG-22
select add_months(sysdate,7) from dual;

-- next_day
-- 오늘 날짜를 기준으로 다음 sunday 가 되는 날짜를 출력
-- 출력 : 30-JAN-22
select next_day(sysdate,'sunday') from dual;

-- last_day
-- 해당 월의 마지막 날짜를 출력
-- 출력 : 31-JAN-22
select last_day(sysdate) from dual;

-- to char
-- 날짜를 문자형태로 변환해 출력
-- 출력 : 2022-01-27
select to_char(sysdate, 'YYYY-mm-dd') from dual;

-- to_date
-- 문자를 날짜로
-- 출력 : 04-DEC-15
select to_date('2015/12/04','yyyy/mm/dd') from dual;

-- nvl
-- NULL 값을 다른 값으로 치환시키는 함수
select nvl(LAST_NAME,'NULL_TO_NOTNULL') from sql_test_a

-- decode
-- switch 문과 같은 역할을 하는듯
-- if / else if  / else 와 같은 역할
-- 첫번째 인자에서 속성을 정해준다.
-- 이후 해당 속성의 값에 대해서, 변환 출력할 수 있는 값을 삽입
-- 만약 if else if 이외에 else 처리를 안해주면 NULL 로 채워진다.
select ID, decode(ID,'1','This is 1','2','This is 2') from sql_test_a;

-- case
-- decode 와 비슷하지만 표현력은 더 좋다.
-- 마지막 END 때문에 많이 헷갈렸는데
-- 작은 따옴표가 아닌 큰 따옴표를 써야 에러가 나지 않는다.

SELECT ID, CASE
             WHEN ID = '1' THEN 'THIS IS 1'
             WHEN ID = '2' THEN 'THIS IS 2'
             WHEN ID = '3' THEN 'THIS IS 3'
             ELSE 'ELSE PART'
          END "THIS IS COL"
  FROM sql_test_a;
```