- 서브쿼리(하위 질의문): where, having절 하위 질의문/from절 하위 질의문(n-tier)

사원의 평균급여보다 많이 받는 직원의 내역을 출력하세요.

```sql
select avg(salary) from employees;
select last_name, salary from employees where salary > (select avg(salary) from employees);
```

- 서브쿼리문 작성 순서

1. 서브쿼리문 작성
2. 메인쿼리문 작성

'Chen' 사원보다 salary를 많이 받는 사원의 목록을 출력하세요.

`select * from employees where salary >(select salary from employees where last_name='Chen');`

'정의찬'과 부서(dept)가 다르지만 동일한 업무(job)을 수행하는 사원 목록을 출력하세요.

'관우'보다 일반화학과목의 학점이 낮은 학생의 명단을 출력하세요.

- having절 서브쿼리

부서 중 가장 급여를 많이 받는 부서를 검색하세요.

```sql
select max(avg(sal)) from emp group by dno

select dno from emp group by dno having avg(sal) = (select max(avg(sal)) from emp group by dno);
```

학생 인원수가 가장 많은 학과를 검색하세요.

```sql
select major, count(*) as cnt from student group by major having count(major) = (select max(count(major)) from student group by major);
```

- 다중 column이나 다중 row에 대한 query

직무(job_id)별 최대급여자의 사원내역을 출력하세요.

```sql
select max(salary) from employees group by job_id;
select employee_id, last_name, salary, job_id from employees where (salary,job_id) in (select max(salary), job_id from employees group by job_id);
```

01번(부서번호) 부서원들과 보너스(comm)가 같은 사원을 검색하세요.

`select * from emp where comm in (select comm from emp where dno = 01);`

- where column = (select ~ ): 단일 row
- where column in (select ~): 다중 row

in: 검색된 값 중에 하나만 일치하면 참

any: 검색된 값의 범위 중에 조건에 맞는 요소가 하나 이상 일치하면 참(or)

all: 검색된 값의 범위 중에 조건에 모두 일치해야 함(and)

- column>max: column>all(subquery) = 가장 큰 값보다 크다.

- column<min: column<all(subquery) = 가장 작은 값보다 작다.

- column>min: column>any(subquery) = 가장 작은 값보다는 크다.

- column<max: column<any(subquery) = 가장 큰 값보다는 작다.

10번 부서에서 가장 작은 급여 수령자보다 더 작은 급여를 수령하는 사람을 검색하세요.

```sql
select min(sal) from emp where dno=10;
select eno, ename, sal, dno from emp where sal<all(select sal from emp where dno=10);
```

30번 부서의 최대급여자보다 급여가 높은 사원을 출력하세요.

`select * from employees where salary > all(select salary from employees where department_id = 30);`

30번 부서의 최대급여자보다 급여가 작은 사원을 출력하세요.

`select * from employees where salary<any(select salary from employees where department_id = 30);`

- from절에 subquery(Top-N SQL)

입사순서가 빠른 5명을 출력하세요.

```sql
select employee_id, last_name, hire_date from employees order by hire_date;
select rownum, alias.* from (select employee_id, last_name, hire_date from employees order by hire_date)alias where rownum<=5;
```

급여 수령액 상위 3명의 사원정보를 출력하세요.

```sql
select rownum, alias.* from (select employee_id, last_name, salary from employees order by salary desc) alias where rownum<=3;
```

- **주의사항**

```sql
create table board(seq number primary key, title varchar2(50), writer varchar2(50), contents varchar2(200), regdate date, hitcount number);
insert into board values("",'a','a','a',sysdate,0);
select * from board order by seq desc;
select * from (select * from board order by seq desc) where rownum between 5 and 8;
```

- 문제해결

```sql
select rownum as row_num, temp.* from (select * from board order by seq desc) temp

select * from (select rownum as row_num, temp.* from (select * from board order by seq desc) temp) where row_num between 5 and 8;
```

paging 처리할 때 중요.