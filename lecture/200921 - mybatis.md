JNDI(Java Naming Directory Interface)를 사용해서 connection pool로 DB 종류를 구분

JPA, hibernate: 객체에 대한 완성도가 높아야 사용할 수 있음. db에서 기본 crud를 다 제공

DAO(Data Access Object): 데이터 접근 객체

DTO(Data Transfer Object), VO(Value Object): 데이터 전달자로 사용됨

framework: 골격이 미리 정해져 있기 때문에 사용 지침서가 있음(사용자가 옵션 선택 가능)

library: 사용 지침서가 없음(기능을 사용자가 사용하기 나름)

dao -> sqlsession -> mybatis config -> mapper -> sql -> db

`${}`: 문자열 대체를 위해서 사용

resultType, resultMap