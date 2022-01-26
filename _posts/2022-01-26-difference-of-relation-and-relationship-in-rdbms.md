---
title: "[RDBMS] DBMS 에서 Relation 과 Relationship 의 차이점"

categories:
  - DBMS
tags: 
  - DBMS
  - RDBMS
  - MySQL
  - Relation
  - Relationship

last_modified_at: 2022-01-26
---

나는 나름대로 MySQL 을 다뤄봤다고 생각했다.

그러나 이 MySQL, 즉 RDBMS 에 대해 깊은 공부를 하지 않은 것 같아 정리를 하고자 한다.

## RDBMS (Relational DataBase Management System)

RDBMS 란 관계형 데이터베이스 관리 시스템으로 관계형 모델을 기반으로 하는 DBMS 유형이다.

그렇다면 관계형 데이터베이스는 무엇일까?

## 관계형 모델이란

관계형 모델은 실제 세계의 데이터를 '관계' 라는 개념을 사용해서 표현한 데이터 모델이다.

## 관계형 데이터베이스란?

관계형 데이터베이스란 테이블(table)로 이루어져 있으며, 이 테이블은 키(key)와 값(value)의 관계를 나타낸다.

이처럼 데이터의 종속성을 관계(relationship)로 표현하는 것이 관계형 데이터베이스의 특징이다.

모든 데이터를 2차원의 테이블 형태로 표현한다.

## 관계형 데이터베이스의 특징

   * 데이터의 분류, 정렬, 탐색 속도가 빠르다.

   * 오랫동안 사용된 만큼 신뢰성이 높고, 어떤 상황에서도 데이터의 무결성을 보장해 준다.

   * 기존에 작성된 스키마를 수정하기가 어렵다.

   * 데이터베이스의 부하를 분석하는 것이 어렵다.


## Relation 이란?

이제 대략적으로 관계형 데이터베이스에 대해 다뤄보았다.

그렇다면 Relation 이란 대체 어떻게 정의해야할까?

> A database consists of a set of tables. A table is also called an entity. 

> It is a basic structure of data in the relational model. 

> A table consists of rows and columns. 

> A row or tuple represents a single entry in the table. 

> The columns represent the attributes.

못난 영어 실력이지만 대충 이해를 할 수 있었다.

![Relation](https://pediaa.com/wp-content/uploads/2018/09/Difference-Between-Relation-and-Relationship-in-DBMS_Figure-1.png)

> 데이터베이스는 하나의 테이블로 구성된다. 이 때 테이블은 Entity (개체) 라고 부를 수 있다. 

> 이것은 관계형 모델에서 데이터의 가장 기본적인 구조다.

> 테이블은 행과 열로 구성되있다.

> 행 또는 튜플은 테이블의 하나의 Entity 를 나타낸다.

> 열은 속성을 나타낸다.

## Relationship 이란?

> Relationship describes how two tables or entities are connected to each other. 

> These tables can be associated with each other using constraints such as primary keys, and foreign keys. 

> A primary key is the main key of a table. 

> It helps to uniquely identify each record in a table. 

> When the primary key in one table is added to some other table, that primary key becomes a foreign key in the new table.

![Relationship](https://pediaa.com/wp-content/uploads/2018/09/Difference-Between-Relation-and-Relationship-in-DBMS_Figure-2.png)

> Relationship 은 두개의 테이블 또는 개체들들이 어떻게 연결되있는지를 설명하는 것이다.

> 이 테이블들은 기본키와 외래키와 같은 제약조건을 사용하여 서로 연관시킬 수 있다.

> 기본키는 테이블의 가장 중심이 되는 키다.

> 이것은 테이블에서 각 Record 를 고유하게 식별하게 해준다.

> 한 테이블의 기본키가 다른 테이블에 추가되면, 해당 기본키는 새 테이블의 외래키가 된다.

## Relation 과 Relationship 의 차이점

오늘 포스팅의 가장 중요한 부분이다.

관계형 관계형 하는데, 그렇다면 RDBMS 에서 Relation 과 Relationship 의 차이점은 무엇일까?

   * 정의
      * Relation
         * 서로 다른 속성으로 구성된 관계형 모델 기반의 데이터베이스의 테이블 혹은 Entity
      * Relationship
         * 관계 모델 기반 데이터베이스에서 두 실체 사이의 연관성을 나타낸다.

   * 추가 사항
      * DBMS 에서 Relation 과 Relaionship 의 또 다른 차이점은, Relation 은 Entity, 즉 개체이며, Relationship은 두 Entities 사이의 관계를 의미한다는 것이다. 

결론적으로 DBMS에서 Relation과 Relationship의 차이점은

   * Relation 은 관계형 모델 데이터베이스의 테이블
   * Relationship 은 관계형 모델 데이터베이스의 두 테이블이 서로 연결되는 방식을 가리킨다는 점이다.

## 관계형 모델과 SQL 의 관련성

   * 관계형 모델 : SQL
   * 릴레이션 : 테이블
   * 튜플 : 행 (Row)
   * 속성 : 칼럼 (Column)


## SQL 로 알아보자

```sql
CREATE TABLE spring5fs.book
(
   `ISBN`         VARCHAR(45)
                    CHARACTER SET utf8
                    COLLATE utf8_general_ci
                    NOT NULL
                    DEFAULT '',
   `TITLE`        VARCHAR(45) CHARACTER SET utf8 COLLATE utf8_general_ci NULL,
   `AUTHOR`       VARCHAR(45) CHARACTER SET utf8 COLLATE utf8_general_ci NULL,
   `GENRE`        VARCHAR(45) CHARACTER SET utf8 COLLATE utf8_general_ci NULL,
   `PUBLISHER`    VARCHAR(45) CHARACTER SET utf8 COLLATE utf8_general_ci NULL,
   `IMAGE`        VARCHAR(45) CHARACTER SET utf8 COLLATE utf8_general_ci NULL,
   `COUNT`        INT(11) NULL DEFAULT 1,
   `SUMMARY`      TEXT CHARACTER SET utf8 COLLATE utf8_general_ci NULL,
   `HIT`          TINYINT(100) NULL DEFAULT 0,
   `DATE`         DATE NULL,
   PRIMARY KEY(`ISBN`)
)
ENGINE INNODB
COLLATE 'utf8_general_ci'
ROW_FORMAT DEFAULT;
```

```sql
CREATE TABLE spring5fs.checkout
(
   `ISBN`               VARCHAR(45)
                          CHARACTER SET utf8
                          COLLATE utf8_general_ci
                          NOT NULL
                          DEFAULT '',
   `TITLE`              VARCHAR(45) CHARACTER SET utf8 COLLATE utf8_general_ci NULL,
   `EMAIL`              VARCHAR(45)
                          CHARACTER SET utf8
                          COLLATE utf8_general_ci
                          NOT NULL
                          DEFAULT '',
   `RENTAL_DATE`        DATETIME NULL,
   `RETURN_DUE_DATE`    DATETIME NULL,
   `EXTENSION_COUNT`    INT(45) NULL DEFAULT 0,
   PRIMARY KEY(`ISBN`, `EMAIL`),
   CONSTRAINT `FK_checkout_1` FOREIGN KEY(`ISBN`)
      REFERENCES book (`ISBN`) ON UPDATE RESTRICT ON DELETE RESTRICT,
   CONSTRAINT `FK_checkout_2` FOREIGN KEY(`EMAIL`)
      REFERENCES member (`EMAIL`) ON UPDATE RESTRICT ON DELETE RESTRICT
)
ENGINE INNODB
COLLATE 'utf8_general_ci'
ROW_FORMAT DEFAULT;
```

내가 프로젝트를 하면서 구현했던 테이블이다.

여기서 Relation 이란 두개의 테이블, 즉 book 과 checkout 인 도서 테이블과 대여 도서 테이블이다.

Relation 은 이 두 테이블의 관계를 의미한다.

```sql
CONSTRAINT `FK_checkout_1` FOREIGN KEY(`ISBN`)
      REFERENCES book (`ISBN`) ON UPDATE RESTRICT ON DELETE RESTRICT,
```

여기서 이 두테이블의 연결점을 볼 수 있다.

book 테이블의 Primary Key 가 checkout 테이블의 외래키로 사용된 것을 볼 수 있다.


## 비고

프로그래밍을 하면서 다양한 테이블을 구현해봤지만, 이 데이터베이스의 기본적인 구성을 다시 한번 생각해볼 수 있었다.

## 참고 사이트

[What is the Difference Between Relation and Relationship in DBMS](https://pediaa.com/what-is-the-difference-between-relation-and-relationship-in-dbms/)