---
title: "[Oracle] 오라클 기본함수 : 문자함수"

categories:
  - oracle
tags: 
  - DBMS
  - SQL
  - Oracle

last_modified_at: 2022-01-27
---

MySQL 과 Oracle 은 비슷하지만 서로 다르다.

요즘은 Oracle를 다시 공부중인데, 공부하면서 실습했던 내용을 정리하고자 한다.

오늘 실습한 문자함수
   * concat
   * initcap
   * lower
   * upper
   * lpad
   * rpad
   * ltrim
   * rtrim
   * substr
   * substrb
   * replace
   * translate
   * trim
   * ascii
   * instr

```sql
-- concat 연결
select concat('hello','bye'), concat('good','bad') from dual;

-- concat ||
select concat('hello','bye') concats, 'good'||'bad' operators from dual;

-- initcap 대문자
select initcap('good morning') from dual;

-- initcap
-- 출력시 Good/Bad Morning 으로 대문자 출력
select initcap('good/bad morning') from dual;

-- lower upper
select lower('GOOD'), upper('good') from dual;

-- LPAD
-- lpad('good',6,'@') -> 6자리에서 글자 없는 부분은 왼쪽에서부터 @ 로 채워줌
select lpad('good',6) "LPAD1", lpad('good',6,'@') from dual;

-- RPAD
-- rpad('good',6,'@') -> 6자리에서 글자 없는 부분은 오른쪽에서부터 @로 채워줌
select rpad('good',6) "RPAD1", rpad('good',6,'@') from dual;

-- LTRIM
-- ltrim('goodbye','go') -> 여기서 go 지만 o 를 다 지워버림 -> dbye 출력
select ltrim('goodbye','g'), ltrim('goodbye','o'), ltrim('goodbye','go') from dual;


-- RTRIM
-- 오른쪽에서부터 지우는 것이기 때문에, 만약 지워야할 문자가 아닌 문자로 분리된 이후에는 지울 수 없다
-- 출력 시 goodeby
select rtrim('goodebye','e') from dual;

-- substr()
select substr('good morning john',8,4) from dual;

-- substr()
-- 8번째 글자부터 4칸
-- rnin 출력
select substr('good morning john',8,4) from dual;

--  - 가 붙을 시 오른쪽에서 부터 센다.
-- john 출력
select substr('good morning john',-4) from dual; 

-- 오른쪽에서 4번째 자리 수부터 2글자 출력
-- jo 출력
select substr('good morning john',-4,2) from dual; 

-- 만약 가장 마지막 인자가 0 인 경우, 그 어떤 값도 가져오지 않는다는 의미다.
-- null 출력
select substr('good morning john',-4,0) from dual;


-- sustrb 의 b 는 byte 를 의미한다.
-- 영어는 상관 없지만, 한글과 같은 경우 substr 과 달라질 수도?
select substrb('good morning john',8,4) from dual; 


-- replace
-- good night tom 출력
select replace('good morning tom','morning','night') from dual;

-- translate
-- we are net alene 출력
-- y -> w 로, o -> e 로, u -> 삭제 와 같이 바꾸겠다는 뜻
select translate('you are not alone','you','we') from dual;

-- trim leading
-- 현재 good 앞에 공백이 있지만 leading 을 통해 공백을 삭제해 줌으로써, length 는 4가 된다.
select length(trim(leading from ' good')) from dual;

-- trim trailing
-- good 뒤에 공백이 있지만 trailing 을 통해 오른쪽 공백을 지움으로써 4가 됨
select length(trim(trailing from 'good    ')) from dual;

-- trim both
-- both 를 통해 앞뒤 모든 공백 삭제 해서, 길이는 4가 됨
select length(trim(both from '       good    ')) from dual;


-- ascii
-- 출력 97
select ascii('a') from dual;


-- instr
-- 1번째 글자서부터 or 이란 글자가 처음 나오는 글자의 숫자
-- 출력 7
select instr('good morning john','or',1) from dual;
```