# 스택

1. [정의](#정의)
2. [특징](#특징)
   1. [Push & Pop](#push--pop)
3. [활용](#활용)
4. [구현](#구현)
5. [시간복잡도와 공간복잡도](#시간복잡도와-공간복잡도)
6. [참고 자료](#참고-자료)

## 정의

> 후입선출(LIFO, Last In First Out) 자료구조.

스택은 **후입선출**의 특성을 갖는 자료구조로 시간 순서상 가장 최근에 추가한 데이터가 가장 먼저 나오는 후입선출 형식으로 데이터를 저장하는 자료구조이다.

## 특징

### Push & Pop

스택은 데이터의 추가/추출을 Push/Pop 연산을 통해 수행한다.

- Push  
  스택의 맨 뒤에 데이터를 추가하면 완료되기에 `O(1)`의 시간복잡도를 갖는다.
- Pop  
  스택 맨 뒤의 데이터를 삭제하면 완료되기에 `O(1)`의 시간복잡도를 갖는다.

두 연산 모두 스택의 top에 원소를 추가/삭제하는 형식으로 구현된다.

## 활용

스택은 **재귀적인 특징**이 있어 소프트웨어 개발 시 자주 사용되는 자료구조이다. 대표적인 활용 예시로 call stack, 후위 표기법 연산, 괄호 유효성 검사, 웹 브라우저 방문기록(뒤로가기), 깊이우선탐색(DFS) 등이 있다.

## 구현

### 큐(Queue) 두 개를 이용한 구현

먼저 두 개의 연산(`push()`, `pop()`)에 사용할 큐들(`q1`, `q2`)을 준비한다.

1. `push()`
   `q1`으로 `enqueue()`를 하여 데이터를 저장한다.
2. `pop()`
   1. `q1`에 저장된 데이터의 수가 1 이하로 남을 때까지 `dequeue()`를 한 후, 추출된 데이터를 `q2`에 `enqueue()`한다. 결과적으로 가장 최근에 들어온 데이터를 제외한 모든 데이터는 `q2`로 옮겨진다.
   2. `q1`에 남아있는 하나의 데이터를 `dequeue()`하여 가장 최근에 저장된 데이터를 반환한다.(LIFO)
   3. 다음에 진행될 `pop()`을 위와 같은 알고리즘으로 진행하기 위해 `q1`과 `q2`의 이름을 swap한다.

큐를 이용해 스택을 구현한 경우에는 시간복잡도가 조금 다르다.

- `push()` : `q1.enqueue()`를 한번 수행하면 되기에 `O(1)`의 시간복잡도를 갖는다.
- `pop()` : `q1`에 저장된 n개의 원소 중 n-1개를 `q2`로 옮겨야 하므로 `O(n)`의 시간복잡도를 갖는다.

## 시간복잡도와 공간복잡도

- 시간복잡도

  |    Operation    | Average | Worst  |
  | :-------------: | :-----: | :----: |
  |     Access      | `Θ(n)`  | `O(n)` |
  |     Search      | `Θ(n)`  | `O(n)` |
  | Insertion(Push) | `Θ(1)`  | `O(1)` |
  |  Deletion(Pop)  | `Θ(1)`  | `O(1)` |

- 공간복잡도  
  `O(n)`

## 참고 자료

- 시간복잡도와 공간복잡도
  - [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)
