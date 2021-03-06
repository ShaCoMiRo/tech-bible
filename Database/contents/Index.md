# 인덱스

1. [인덱스(Index)란?](#인덱스index란)
2. [인덱스의 구조](#인덱스의-구조)
   1. [해시 테이블](#해시-테이블)
   2. [B+Tree](#btree)
3. [인덱스의 구분](#인덱스의-구분)
4. [인덱스의 장단점](#인덱스의-장단점)
   1. [장점](#장점)
      1. [조건 검색(`SELECT ~ WHERE ~`) 속도 향상](#조건-검색select--where--속도-향상)
      2. [정렬(`ORDER BY ~`) 속도 향상](#정렬order-by--속도-향상)
      3. [MIN, MAX의 효율적인 처리](#min-max의-효율적인-처리)
   2. [단점](#단점)
      1. [데이터 변경(DML)에 취약](#데이터-변경dml에-취약)
      2. [모든 상황에서 인덱스 스캔이 유리하지는 않음](#모든-상황에서-인덱스-스캔이-유리하지는-않음)
      3. [추가적인 저장 공간이 필요](#추가적인-저장-공간이-필요)
5. [인덱스 생성 전략](#인덱스-생성-전략)
6. [참고 자료](#참고-자료)

## 인덱스(Index)란?

인덱스는 **데이터베이스에서 테이블의 검색 성능을 높여주는 자료구조**이다. 일반적인 RDBMS에서는 **B+Tree** 구조로 된 인덱스를 사용하여 검색 속도를 향상시킨다.

인덱스는 책마다 있는 **색인**과 같은 역할을 한다. 책에서 원하는 내용을 찾을 때 처음부터 끝까지 훑어보는(**Full Table Scan**) 대신 색인을 살펴보면 어느 페이지에 원하는 내용이 있는지 바로 찾을 수 있는 것(**Index Scan**)과 비슷하다.

`SELECT ~ WHERE` 쿼리를 통해 특정 조건을 만족하는 데이터를 찾을 때, Full Table Scan 할 필요 없이 **정렬되어 있는 인덱스에서 훨씬 빠른 속도로 검색**을 할 수 있게 된다.

![[DB] 데이터베이스(DB) 인덱스(Index) 란 무엇인가?-INDEX_OVERVIEW](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbPb8pb%2FbtrePWRO9HY%2FqrzMfX84KAAuFgkyZkKtKK%2Fimg.png)

## 인덱스의 구조

인덱스는 B\*Tree, B-Tree, B+Tree, Hash, Bitmap 등으로 구현될 수 있다. 많은 데이터베이스 시스템은 인덱스를 B+Tree 구조로 가진다.

인덱스를 생성하게 되면 특정 칼럼(Column)의 값을 기준으로 **정렬**하여 데이터의 **물리적 위치**와 함께 별도의 파일에 저장한다. 이 때, 인덱스에 저장되는 속성 값을 `search-key` 값이라 하고 실제 데이터의 물리적 위치를 저장한 값을 `pointer`라고 한다.

즉, 인덱스는 순서대로 정렬된 `search-key` 값과 `pointer` 값만 저장하기 때문에 **테이블보다 적은 공간을 차지**한다. 보통 인덱스는 테이블 크기의 10% 정도의 저장공간을 차지한다.

### 해시 테이블

해시 테이블은 key-value로 데이터를 저장하는 자료구조 중 하나로, 해시 함수를 활용한다. 해시 테이블을 활용하면 <b>단일 데이터를 탐색하는 시간이 `O(1)`</b>로 B+Tree보다 빠르지만, 등호(=) 연산에만 특화되고 부등호 연산(>, <)이 자주 사용되는 쿼리에서는 매우 비효율적이기에 **인덱스에 사용하기엔 적합하지 않다.**

### B+Tree

B+Tree는 균형이진탐색트리의 일종으로, B-Tree를 개선한 것이다. B+Tree가 해시 테이블 대신 데이터베이스 인덱스 구현에 사용되는 이유는 다음과 같다.

1. 항상 정렬된 상태를 특정 값보다 크고 작은 부등호 연산에 문제가 없다.
2. 데이터 탐색뿐 아니라 저장, 수정, 삭제에도 항상 `O(log(n))`의 시간복잡도를 갖는다.

## 인덱스의 구분

- **클러스터형 인덱스(Clustered Index)**
  - 특정 칼럼을 **기본키(Primary Key)로 지정**하면 자동으로 클러스터형 인덱스가 생성되고, 해당 칼럼을 기준으로 정렬된다.
  - **테이블 자체가 정렬된 하나의 인덱스**이다.
    - 영어사전처럼 책의 내용 자체가 정렬된 것에 비유할 수 있다.
- **넌클러스터형 인덱스(Nonclustered Index)**
  - 일반 책의 찾아보기와 **같이 별도의 공간에 인덱스가 생성**된다.
  - `CREATE INDEX`와 같이 **인덱스를 생성**하거나, **고유키(Unique Key)로 지정**하면 보조 인덱스가 생성된다.

## 인덱스의 장단점

인덱스의 가장 큰 특징은 **데이터들이 정렬되어 있다**는 점이다. 이 특징은 조건 검색이라는 영역에서 굉장한 장점이 된다. 인덱스의 주요 장점들 모두 데이터들이 정렬되었다는 장점을 관통하는 내용들이다.

### 장점

#### 조건 검색(`SELECT ~ WHERE ~`) 속도 향상

테이블을 만들고 안에 데이터가 쌓이게 되면 테이블의 레코드(Record)는 내부적으로 순서가 없이 뒤죽박죽으로 저장된다. 이렇게 되면 WHERE절에 특정 조건에 맞는 데이터들을 찾아낼 때도 레코드의 처음부터 끝까지 다 읽어서 검색 조건과 맞는지 비교해야 한다. 이것을 풀 테이블 스캔(**Full Table Scan**), 줄여서 풀 스캔(Full Scan)이라고 한다.

반면에 **인덱스 테이블 스캔(Index Table Scan) 시 인덱스 테이블은 데이터들이 정렬되어 저장되어 있기 때문에 검색 조건(WHERE)에 맞는 데이터들을 빠르게 찾아낼 수 있다.** 이것이 인덱스를 사용하는 가장 큰 이유이다.

#### 정렬(`ORDER BY ~`) 속도 향상

인덱스를 사용하면 ORDER BY 절에 의한 정렬(Sort) 과정을 피할 수 있다. ORDER BY는 부하가 굉장히 많이 걸리는 작업이다. 정렬과 동시에 1차적으로 메모리에서 정렬이 이루어지고, 메모리보다 큰 작업이 필요하다면 디스크 I/O도 추가적으로 발생되기 때문이다.

하지만 인덱스를 사용하면 이러한 전반적인 자원의 소모를 피할 수 있다. 이미 정렬되어 있기 때문에 가져오기만 하면 되기 때문이다.

#### MIN, MAX의 효율적인 처리

이 역시 데이터가 정렬되어 있기에 얻을 수 있는 장점이다. MIN 값과 MAX 값을 레코드의 시작 값과 끝 값 한 건씩만 가져오면 되기 때문에 Full Table Scan으로 테이블을 모두 뒤져서 작업하는 것보다 훨씬 효율적으로 찾을 수 있다.

### 단점

#### 데이터 변경(DML)에 취약

SELECT가 아닌 INSERT, UPDATE, DELETE를 통해 **데이터가 추가되거나 값이 바뀐다면 인덱스 테이블 내에 있는 값들을 다시 정렬(재구성)해야 한다.** 또한 인덱스 테이블, 원본 테이블 이렇게 두 군데의 데이터를 수정하는 작업을 진행해야 한다는 단점도 있다. 때문에 DML이 빈번한 테이블보다 검색을 위주로 하는 테이블에 인덱스를 생성하는 것이 좋다.

#### 모든 상황에서 인덱스 스캔이 유리하지는 않음

검색을 위주로 하는 테이블에 인덱스를 생성하는 것이 좋지만, 무조건 검색 시에도 인덱스가 좋다고 말할 수는 없다. **인덱스는 테이블의 전체 데이터 중에서 10~15% 이하의 데이터를 처리하는 경우에만 효율적이고, 그 이상의 데이터를 처리할 땐 인덱스를 사용하지 않는 것이 더 낫다.**

직관적인 예시를 들자면 1개의 데이터가 있는 테이블A와 100만 개의 데이터가 있는 테이블B가 있다고 가정했을 때, 테이블A는 풀 스캔보다 인덱스 스캔이 유리하겠으나 테이블B는 굳이 인덱스 스캔을 사용하지 않고 풀 스캔을 사용하더라도 충분히 빠를 것이다.

#### 추가적인 저장 공간이 필요

**인덱스를 관리하기 위해서는 데이터베이스의 약 10%에 해당하는 저장공간이 추가로 필요**하다. 무턱대고 속도 향상을 위해 인덱스 생성을 남발하면 저장공간이 그만큼 낭비되는 상황이 발생하므로 비용을 잘 계산해야 한다.

## 인덱스 생성 전략

인덱스를 가장 효율적으로 사용하려면 다음 조건들을 고려해야 한다.

- 조건절(`WHERE`)에 자주 사용되는 칼럼
- 데이터 수정 빈도가 낮은 칼럼
  - INSERT, UPDATE, DELETE 작업 시 인덱스에서 매번 정렬을 수행해야 하므로, 수정 빈도가 낮아야 효율적이다.
- 중복되는 데이터가 최소한인 칼럼
  - 성별과 같이 2종류의 값만 존재하는 칼럼은 비효율적이다. 즉, 선택도가 낮을 때 유리하다.
- 테이블의 데이터 양이 매우 많은 경우
- JOIN 조건으로 자주 사용되는 칼럼
- ORDER BY 조건으로 자주 사용되는 칼럼
- 항상 =으로 비교되는 칼럼
- 단일 테이블은 적정 인덱스 개수를 유지

표로 간단히 요약하면 다음과 같다.

| 기준                    | 적합성                                        |
| ----------------------- | --------------------------------------------- |
| 카디널리티(Cardinality) | 높을수록 적합(데이터 중복이 적을수록 적합)    |
| 선택도(Selectivity)     | 낮을수록 적합                                 |
| 조회 활용도             | 높을수록 적합(WHERE절에서 자주 사용되면 적합) |
| 수정 빈도               | 낮을수록 적합                                 |

> - 카디널리티
>   - 데이터가 중복되지 않는 정도
> - 선택도
>   - 데이터에서 특정값을 잘 골라낼 수 있는 정도
>   - 선택도가 1이면 모든 데이터가 Unique함을 의미한다.

## 참고 자료

- [[Database] 인덱스(index)란?](https://mangkyu.tistory.com/96)
- [[DB] 11. 인덱스(Index) - (1) 개념, 장단점, B+Tree 등](https://rebro.kr/167)
- [[DB] 데이터베이스(DB) 인덱스(Index) 란 무엇인가?](https://choicode.tistory.com/27)
- [[자료구조] 간단히 알아보는 B-Tree, B+Tree, B\*Tree](https://ssocoit.tistory.com/217)
- [[DB] 인덱스 자료 구조 (B-Tree)](https://velog.io/@sem/DB-%EC%9D%B8%EB%8D%B1%EC%8A%A4-%EC%9E%90%EB%A3%8C-%EA%B5%AC%EC%A1%B0-B-Tree)
