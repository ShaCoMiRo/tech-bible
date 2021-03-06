# RDB와 NoSQL의 차이

1. [두 데이터베이스 유형의 차이를 알아둬야 하는 이유](#두-데이터베이스-유형의-차이를-알아둬야-하는-이유)
2. [RDB(관계형 데이터베이스)](#rdb관계형-데이터베이스)
3. [NoSQL(비관계형 데이터베이스)](#nosql비관계형-데이터베이스)
4. [비교](#비교)
5. [확장성](#확장성)
6. [사용해야 하는 경우](#사용해야-하는-경우)
   1. [RDB](#rdb)
   2. [NoSQL](#nosql)
7. [참고 자료](#참고-자료)

## 두 데이터베이스 유형의 차이를 알아둬야 하는 이유

현재 RDB가 더 많이 쓰이지만 NoSQL을 도입하는 영역이 넓어지고 있는 추세다. 데이터베이스는 단순히 프레임워크에 따라 결정하는 것이 아닌, RDB와 NoSQL 중 **프로젝트에 더 적합한 데이터베이스를 채택**해야 한다. 이를 위해서는 각 방식의 장단점과 차이점을 파악하고 있어야 한다.

## RDB(관계형 데이터베이스)

- SQL을 사용하여 RDBMS를 통해 데이터를 저장, 수정, 삭제 및 검색할 수 있다.
- 관계형 데이터베이스에는 핵심적인 두 가지 특징이 있다.
  1.  데이터는 **정해진 데이터 스키마에 따라 테이블에 저장**된다.
  2.  데이터는 **관계를 통해 여러 테이블에 분산**된다.

데어터는 테이블에 레코드로 저장되는데, 각 테이블마다 명확하게 정의된 구조가 있다. 해당 구조는 필드의 이름과 데이터 유형으로 정의된다.

따라서 **스키마를 준수하지 않은 레코드는 테이블에 추가할 수 없다.** 즉, 스키마를 수정하지 않는 이상은 정해진 구조에 맞는 레코드만 추가가 가능한 것이 관계형 데이터베이스의 특징 중 하나이다.

또한, 데이터의 중복을 피하기 위해 관계를 이용한다. 하나의 테이블에서 중복 없이 하나의 데이터만을 관리하기 때문에 다른 테이블에서 부정확한 데이터를 다룰 위험이 줄어드는 장점이 있다.

## NoSQL(비관계형 데이터베이스)

- 말 그대로 관계형 DB의 반대이다.
- 스키마가 없으며, 관계도 없다.
- NoSQL에서는 레코드를 문서(documents)라고 부른다.
  - 문서는 JSON 포맷과 유사한 형태를 갖고 있다.
- **key-value storage System**을 사용한다.
  - SQL과 트랜잭션을 지원하지 않는 특징이 있기 때문에 **NoSQL System**이라고도 불린다.

NoSQL이 RDB와 구분되는 핵심적인 차이점은 **key-value storage 시스템을 사용**한다는 점이다. key-value storage 시스템은 데이터를 key-value 형태를 가지고 있는 문서로 작성해서 컬렉션에 넣는 방식이다.

기존 RDB에서 다수의 테이블을 관계로 연결지었다면, NoSQL에서는 하나의 컬렉션에 모든 데이터를 key-value 형태로 담는다. 즉, 여러 테이블에 조인할 필요 없이 이미 필요한 모든 것을 갖춘 문서를 작성하는 것이 NoSQL이다.

NoSQL에는 Bigtable, DynamoDB, Cassandra, MongoDB 등이 있다. 그 중 MongoDB의 예시를 통해 NoSQL의 동작 원리를 살펴보면 다음과 같다.

```
//컬렉션 생성
db.createCollection("studnet")

//key-value 쌍으로 구성된 JSON 포맷으로 데이터를 작성하여 삽입
db.student.insert("id": 2022394, "name": "Nossi", "class": ["Math", "Eng"])
db.student.insert("id": 2021921, "name": "Bob", "class": ["Eng"])


db.student.find()                     //모든 데이터 조회
db.student.findOne({"id": 2022394})   //단일 데이터 조회


db.student.remove({"name": "Nossi})   //단일 데이터 삭제
db.student.drop()                     //단일 컬렉션 제거
```

## 비교

두 데이터베이스 유형의 주요 차이점을 정리하면 다음과 같다.

|                  | RDB(SQL)                                                                                                                                                                                                 | NoSQL                                                                                                                                                                                                                                                                                             |
| :--------------: | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 데이터 저장 모델 | 테이블                                                                                                                                                                                                   | json document / key-value / 그래프 등                                                                                                                                                                                                                                                             |
|    개발 목적     | 데이터 중복 감소                                                                                                                                                                                         | 애자일 / 확장 가능성 / 수정 가능성                                                                                                                                                                                                                                                                |
|      스키마      | **엄격한** 데이터 구조                                                                                                                                                                                   | **유연한** 데이터 구조                                                                                                                                                                                                                                                                            |
|       장점       | <ul><li>**명확한** 데이터 구조(스키마)를 보장한다.</li><li>데이터 중복 없이 한 번만 저장되어 **무결성**을 보장한다.</li><li>데이터 중복이 없어 **데이터 Update가 용이**하다.</li></ul>                   | <ul><li>스키마가 없어 **유연**하고 **자유**로운 데이터 구조를 갖고 있다.</li><li>새로운 필드 추가가 자유롭다.</li><li>데이터는 애플리케이션이 필요로 하는 형식으로 저장되며, 데이터 읽기 속도가 빨라진다.</li><li>**수직적 확장**(Scale Up)과 **수평적 확장**(Sacle Out) 모두 용이하다.</li></ul> |
|       단점       | <ul><li>시스템이 커지면 조인문이 많은 **복잡한 쿼리가 필요**하다.</li><li>수평적 확장이 까다로워 비용이 큰 **수직적 확장**(Scale Up)이 주로 사용된다.</li><li>데이터 구조가 **유연하지 않다**.</li></ul> | <ul><li>데이터 중복이 발생할 수 있으며, 이를 계속 갱신해야 한다.</li><li>**중복 데이터가 많기 때문에 데이터 변경 시 모든 컬렉션에서 수정이 필요**하다.</li><li>명확한 데이터 구조를 **보장하지 않는다**.</li></ul>                                                                                |
|       사용       | <ul><li>**데이터 구조가 변경될 여지가 없이 명확**한 경우</li><li>**데이터 Update가 잦은** 시스템<ul><li>중복 데이터가 없으므로 변경에 유리</li></ul></li></ul>                                           | <ul><li>정확한 데이터 구조가 정해지지 않은 경우</li><li>**Update가 자주 이루어지지 않는 경우**</li><li>데이터의 양이 매우 많은 경우(=조회가 많은 경우)<ul><li>수평적 확장(Scale Out) 가능</li></ul></li></ul>                                                                                     |

## 확장성

두 데이터베이스 유형을 비교할 때는 Scaling(확장성) 개념도 중요한 기준 중 하나이다.

데이터베이스 서버의 확장은 <b>수직적 확장(Sacle Up)</b>과 <b>수평적 확장(Scale Out)</b>으로 나뉜다.

- 수직적 확장 : 단순히 데이터베이스 서버의 성능을 향상시키는 것을 의미한다.(CPU 업그레이드 등)
- 수평적 확장 : 더 많은 서버가 추가되고 데이터베이스가 전체적으로 분산됨을 의미한다.(하나의 데이터베이스에서 작동하지만, 여러 호스트에서 작동)

RDB는 ACID와 트랜잭션을 보장하기 위해서 수평적 확장이 쉽지 않다. 또한 다수의 서버로 수평적 확장을 할 경우 조인을 하기 위해 굉장히 복잡한 과정이 필요하다.

RDB를 수평적 확장하려면 샤딩(Sharding; 데이터가 수평적으로 분할되고 기기의 모음 전반에 걸쳐 분산되는 경우)이 필요하다. ACID 준수를 유지하며 RDB를 샤딩하는 것은 매우 까다로운 작업이다.

NoSQL은 ACID, 트랙잭션을 지원하지 않으므로 수평적 확장이 수월하다.

## 사용해야 하는 경우

### RDB

- 데이터 구조가 명확하여 변경될 여지가 없는 경우.
- 관계를 맺고 있는 데이터의 변경이 잦은 경우.

### NoSQL

- 정확한 데이터 구조를 알 수 없거나 변경/확장될 수 있는 경우.
- 데이터 조회가 잦지만 변경은 드문 경우.
- 막대한 양의 데이터를 다루어 데이터베이스를 수평으로 확장해야 하는 경우.

## 참고 자료

- [SQL과 NOSQL의 차이](https://gyoogle.dev/blog/computer-science/data-base/SQL%20&%20NOSQL.html)
- [SQL vs NoSQL](https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Database/SQL%20vs%20NoSQL.md)
