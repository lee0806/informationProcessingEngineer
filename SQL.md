
**용어 정리**

**Attribute (속성)** : 테이블에서 하나의 열(세로)(Column) - 데이터의 특성
**Turple (튜플)** : 테이블에서 하나의 행(가로)(Row) - 한 사람의 데이터 묶음
**Degree (차수)** : 한 릴레이션(테이블)에 존재하는 속성(Attribute)의 개수
**Cardinality (기수)** : 한 릴레이션(테이블)에 존재하는 튜플(Tuple)의 개수
**Domain (도메인)** : 하나의 속성에 들어갈 수 있는 값의 범위 또는 유형 (학번은 7자리의 숫자, 이름은 한글 문자열, 학과는 지정된 학과명 등등... )
**Schema (스키마)** : 데이터베이스 전체의 논리적 설계도 - 구조, 제약 조건, 관계 등을 정의
**Instance (인스턴스)** : 특정 시점에서 실제로 저장된 데이터의 모음 (스냅샷)

**Key (키)** : 특정 튜플(행)을 식별하기 위해 사용하는 속성
**Primary Key (기본키)** : 튜플을 고유하게 식별할 수 있는 속성 (ex. id)
**Candidate Key (후보키)** : 기본키가 될 수 있는 후보 속성 (ex. id, 학번, 등등)
**Alternate Key (대체키)** : 후보키 중에서 기본키로 선택되지 않은 키
**Foreign Key (외래키)** : 다른 테이블의 기본키를 참조하는 속성
**Super Key (슈퍼키)** : 튜플을 유일하게 식별할 수 있는 속성들의 집합 (중복해서 가능, 이름 + 전화번호, 기본키도 슈퍼키에 포함은 됨)
**Relation (릴레이션)** : 행과 열로 구성된 2차원 테이블
**Integrity (무결성)** : 데이터의 정확성과 일관성을 유지하기 위한 제약조건




### 0. 테이블 만들기 / 지우기 (DDL)

**CREATE TABLE - 테이블 만들기**

```
CREATE TABLE 학생 (
	id     INT,
	이름    VARCHAR(20),
	나이    INT,
	반      CHAR(1)
)


```

- INT : 정수 숫자
- VARCHAR(20) : 글자 (최대 20글자)
- CHAR(1) : 1글자

**DROP TABLE - 테이블 지우기**

```
DROP TABLE 학생;
```

- 테이블 자체를 삭제, 복구가 어려움

**ALTER TABLE - 테이블 수정하기**

```
-- 컬럼(열) 추가
ALTER TABLE 학생 ADD 학점 VARCHAR(2);

-- 컬럼(열) 지우기
ALTER TABLE 학생 DROP COLUMN 학점;
```

**CASCADE**

- CASCADE 옵션을 사용하여 연쇄적으로 묶여 있는것들을 전부 삭제

### 1. 데이터 넣기 / 바꾸기 / 지우기 (DML : INSERT / UPDATE / DELETE)

**INSERT - 행(ROW) 추가**

```
INSERT INTO 학생 (id, 이름, 나이, 반)
VALUES (1, '민지', 10, 'A');

INSERT INTO 학생 (id, 이름, 나이, 반)
VALUES (2, '철수', 12, 'A');

INSERT INTO 학생 (id, 이름, 나이, 반)
VALUES (3, '영희', 11, 'B');
```

**UPDATE - 값  바꾸기**

```
-- id가 2번인 학생의 반을 B로 바꾸기
UPDATE 학생 SET 반 = 'B'
WHERE id = 2;
```

SET 뒤에는 바꿀 값을 작성 "바꿀 열값에 새값 삽입"
WHERE 문이 없으면 해당하는 열을 모두 바꾸니 조건을 꼭 달아야됨

**DELETE - 행 지우기**

```
-- id가 3번인 학생 삭제
DELETE FROM 학생
WHERE id = 3;
```

조건이 없으면 테이블 안에 데이터가 다 사라짐

### 2. 데이터 조회 (보기) - SELECT

**SELECT - 기본 검색**

```
-- 모든 열 보기 * 는 모든 컬럼을 조회
SELECT * FROM 학생(테이블);

-- 원하는 열만 보기
SELECT 이름, 나이(COLOMN) FROM 학생;
```

 **WHERE - 조건(필터)**

```
-- 학생 테이블에서 나이가 11 이상인 학생 이름과 나이 검색
SELECT 이름 나이
FROM 학생
WHERE 나이 >= 11;

-- 학생 테이블에서 반이 'A'인 학생 이름과 나이 검색
SELECT 이름, 나이
FROM 학생
WHERE 반 = 'A';
```

**AND / OR / NOT - 조건 조합**

```
-- 학생 테이블에서 반이 'A'이면서 나이가 11이상인 열 전체 조회
SELECT *
FROM 학생
WHERE 반 = 'A' AND 나이 >= 11;

-- 반이 'A'이거나 나이가 12
SELECT *
FROM 학생
WHERE 반 = 'A' OR 나이 = 12;

-- 반이 'A'가 아닌 학생
SELECT *
FROM 학생
WHERE NOT 반 = 'A';
```

**LIKE - 글자 패턴 찾기**

```
-- 이름에 '영'이 들어가는 학생 
SELECT * 
FROM 학생
WHERE 이름 LIKE '%영%';

-- 두 번째 글자가 'ㅈ'인 형태 (영문 예시 : '_o%')
-- '_' = 글자 1개, '%' = 글자 0 ~ N개
```

**NULL - 값이 비어 있음**

```
-- WHERE 컬럼 IS NULL / IS NOT NULL로 확인
-- 비어있는가, 안비어있는가 확인
SELECT *
FROM 학생
WHERE 학생 IS NULL;
```

- 학점 = NULL로 쓰지 않음 -> IS NULL 사용

**DISTINCT - 중복 제거**

```
-- 중복된 반 이름은 1번만 보기
SELECT DISTINCT 반
FROM 학생;
```

**ORDER BY - 정렬**

```
-- 나이 오름차순 (작은 수 -> 큰 수)
SELECT 이름, 나이
FROM 학생
ORDER BY 나이 ASC; -- ASC는 생략할 수 있음

-- 나이 내림차순 (큰 수 -> 작은 수)
SELECT 이름, 나이
FROM 학생
ORDER BY 나이 DESC;

-- 반 오름차순 후 나이 내림차순
SELECT 이름, 반, 나이
FROM 학생
ORDER BY 반 ASC, 나이 DESC;
```

### 3. COUNT / SUM / AVG + GROUP BY / HAVING -  계산 

**전체 개수 세기**

```
SELECT COUNT(*) AS 전체 명수
FROM 학생;
```

**그룹으로 묶기 - GROUP BY**

```
-- 반별 학생 수
SELECT 반, COUNT(*) AS 인원수
FROM 학생
GROUP BY 반;
```

**그룹 조건 - HAVING**

```
-- 반별 학생 수가 2명 이상인 반만
SELECT 반, COUNT(*) AS 인원수
FROM 학생
GROUP BY 반
HAVING COUNT(*) >= 2;
```

WHERE(행 필터) -> GROUP BY (묶기) -> HAVING (필터) -> ORDER BY (정렬)



#### 문제 1


다음 중 employee 테이블에서
직급(job)이 'MANAGER'인 사람의 이름(ename)과 급여(sal)를 출력하시오.
단, 급여가 **3000 이상**인 경우만 출력한다.

![[스크린샷 2025-10-30 오후 2.24.08.png]]

내 정답 ✅ 
> SELECT ename, sal FROM employee WHERE job = "MANAGER" and sal >= 3000

> 표준 SQL에서는 작은 따옴표 ''를 사용, 조건 연결 and이므로
> SELECT ename, sal FROM employee WHERE job = 'MANAGER' AND sal >= 3000

#### 문제 2

각 부서(deptno)별 평균 급여를 구하고,
그 평균이 **2500 이상인 부서만** 출력하시오.

![[스크린샷 2025-10-30 오후 2.25.59.png]]
![[스크린샷 2025-10-30 오후 2.26.08.png]]

내 정답 ❌
> ...

정답  ✅
> SELECT deptno, AVG(sal) AS avg_sal FROM employee GROUP BY deptno HAVING AVG(sal) >= 2500;

> 1. GROUP BY를 통해 부서별로 묶음
> 2. HAVING을 AVG의 결과를 사용

#### 문제 3


employee 테이블과 dept 테이블을 조인하여
직원 이름(ename)과 소속 부서 이름(dname)을 출력하시오.

내 정답 ❌
> SELECT ename, dname FROM JOIN employee, dept

정답 ✅ 
> SELECT e.ename, d.dname FROM employee e JOIN dept d ON e.deptno = d.deptno;

> ON은 JOIN 조건으로 JOIN 조건이 없을 경우 모든 속성이 곱해지기 때문에 조건을 달아줘야함
> employee와 dept이 중복된 값 deptno 값을 조인 조건으로 설정하여 JOIN을 진행


#### 문제 4

급여(sal)가 전체 직원의 평균 급여보다 높은 직원의 이름(ename)과 급여(sal)을 출력하시오.

내 정답 🟡
> SELECT ename, sal FROM employee WHERE sal >= 평균급여

정답 ✅ 
> SELECT ename, sal FROM WHERE sal >= (SELECT AVG(sal) FROM employee);

> 서브 쿼리를 작성해 평균 급여를 계산

#### 문제 5

다음 employee 테이블에서,
**각 부서별로 최고 급여(sal)를 받는 직원의 이름(ename), 부서번호(deptno), 급여(sal)**를 출력하시오.
단, **서브쿼리(subquery)**를 사용할 것.

|**ename**|**sal**|**deptno**|
|---|---|---|
|SMITH|800|20|
|ALLEN|1600|30|
|WARD|1250|30|
|JONES|2975|20|
|BLAKE|2850|30|
|CLARK|2450|10|
|KING|5000|10|

출력 예시

| **ename** | **deptno** | **sal** |
| --------- | ---------- | ------- |
| KING      | 10         | 5000    |
| JONES     | 20         | 2975    |
| BLAKE     | 30         | 2850    |
```
SELECT e.ename, e.deptno, e.sal
FROM employee e
JOIN (
  SELECT deptno, MAX(sal) AS max_sal
  FROM employee
  GROUP BY deptno
) m
  ON e.deptno = m.deptno
 AND e.sal = m.max_sal;
```

> 1. SELECT : 선택한다 e.ename과 e.deptno, e.sal을
> 2. FROM : employee(e)에서 
> 3. JOIN : 합친다.
> 4. SELECT deptno, MAX(sal) AS max_sal FROM employee GROUP BY deptno
> 5. deptno의 중복을 제거하고(그룹으로 묶고) employee에서 deptno와 sal의 최댓값을 선택하고
> 6. 거기서 e.deptno와 m.deptno가 같고 e.sal이 m.max_sal이 같은 값만 


2025.10.31.

문제 1

EMPLOYEE 테이블에서 DEPTNO가 30인 직원의 이름(ENAME)과 급여(SAL)를 출력하시오.
단, 급여는 내림차순으로 정렬하시오.

```
SELECT ename, sal FROM employee WHERE deptno = 30 ORDER BY sal DESC;
```

문제 2

EMPLOYEE 테이블에서 부서별(DEPTNO) 평균 급여(AVG(SAL))를 구하고,

평균 급여가 **2500 이상인 부서**만 출력하시오.

결과는 평균 급여의 내림차순으로 정렬하시오.

```
SELECT deptno, AVG(sal) FROM employee GROUP BY deptno HAVING AVG(sal) >= 2500 ORDER BY AVG(sal) DESC;

```

문제 3

EMPLOYEE 테이블과 DEPT 테이블을 조인하여,

직원 이름(ENAME)과 부서 이름(DNAME)을 출력하시오.

단, 부서번호(DEPTNO)가 일치하는 경우만 출력하시오.

```
SELECT e.ename, d.dname FROM employee e JOIN dept d ON e.deptno = d.deptno;
```


문제 4

EMPLOYEE 테이블에서 **전체 평균 급여보다 높은 급여를 받는 직원의 이름과 급여**를 출력하시오.

결과는 급여 기준으로 내림차순 정렬하시오.

```
SELECT ename, sal FROM employee WHERE sal > (SELECT AVG(sal) FROM employee) ORDER BY sal DESC;
```


문제 5

EMP30 테이블에는 **30번 부서 직원**,

EMP40 테이블에는 **40번 부서 직원**이 저장되어 있다.

두 테이블에 모두 존재하는 직원(ENAME)의 이름을 출력하시오.

모르겠음

```
SELECT a.ename FROM EMP30 a JOIN EMP40 b ON a.ename = b.ename;
```