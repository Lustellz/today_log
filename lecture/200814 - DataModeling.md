- 트리거(Trigger): 특정 테이블의 데이터에 변경이 이루어졌을 때 자동으로 다른 어떤 작업이 함께 수행되도록 설정하기 위해 생성

```sql
create table emp11(empno number primary key,
                  ename varchar2(20),
                  job varchar2(20));
                  
create or replace trigger trg_01 after insert on emp11
begin dbms_output.put_line('신입 사원이 추가되었습니다.');
end;

insert into emp11 values(1, '홍길동', '개발');
```

- 트리거 유형: 문장 레벨(DML문을 실행할 때 단 한 번만 실행), 행 레벨 트리거(FOR EACH ROW, DML문을 여러번 실행하면 여러 번 수행)

```sql
create table sal01(salno number primary key, sal number, empno number references emp11(empno));

create sequence sal01_salno_seq;

create or replace trigger trg02 after insert on emp11 for each row begin insert into sal01 values(sal01_salno_seq.NEXTVAL,10000,:NEW.empno);
end;
```

- 트리거에서 insert, update할 때 기존 값을 `:OLD`, 현재 입력하고 있는 값을 `:NEW`라고 선언

사원이 삭제되면 그 사원의 급여정보(sal01) 테이블에서 해당 row도 함께 삭제하게 되도록 트리거를 구현해 보세요.

```plsql
create or replace trigger trg02 after insert on emp11 for each row begin insert into sal01 values(sal01_salno_seq.NEXTVAL,10000,:NEW.empno); end;

insert into emp11 values(3, '홍길동2', '개발');

create or replace trigger trg03 after delete on emp11 for each row begin delete from sal01 where empno=:OLD.empno; end;

delete from emp11 where empno=3;
```

JPA, hibernate

- 엔티티 타입의 특징

1. 사용자 입장에서 반드시 필요한 정보
2. 유일한 식별자에 의해 식별이 가능
3. 영속적으로 존재하는 엔티티의 집합
4. 프로세스에 의해 이용
5. 반드시 속성이 존재
6. 다른 엔티티타입과 최소 한 개 이상의 관계가 존재

주식별자(N:N)-비식별자(join 횟수 증가), 보조식별자, 내부식별자, 외부식별자, 단일식별자, 복합식별자, 원조식별자, 대리식별자

1:N 관계, N:M 관계

관계(Data): Entity