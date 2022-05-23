# Two Pointers(투 포인터)

명칭대로 **두개의 포인터를 사용하여 문자열이나 배열(혹은 리스트)에서 원하는 값을 찾거나 반복문을 사용하는 경우 사용하는 알고리즘**이다.

**시간 복잡도를 O(N^2)에서 O(N)으로 단축**시킬 수 있는 방법으로, 메모리를 절약하고 시간 효율성을 높일 수 있어 **반복문으로 단순 탐색하면 시간 초과가 걸리는 경우에 유용**하다. 코딩 테스트에서 주어지는 테스트 케이스의 길이 `n`이 매우 큰 경우 `Time out`이 발생하곤 하는데, 이럴 때 사용을 염두해볼만 하다.

포인터는 크게 두가지 방식으로 쓰인다.

1. 앞 포인터와 끝 포인터가 각 위치에서 시작해서 중간에서 만나는 형식.
2. 빠른 포인터(Fast runner)가 느린 포인터(Slow runner)보다 앞서는 형식.

## 중간에서 만나는 포인터

대표적으로 '구명 보트' 문제가 있다.

이 문제는 원래대로라면 2중 for문을 활용해서 두 사람의 무게합이 `limit`보다 작은지를 확인하고 보트에 태워야 한다. 그러나 배열 `people`의 길이에 따라 반복 횟수가 증가하고, 이미 태웠는지 여부를 계속 확인해야 하는 불편함이 있다.

```java
public int solution(int[] people, int limit) {
    int answer = 0;
    int lt = 0;
    int rt = people.length - 1;
    Arrays.sort(people);

    while(lt <= rt) {
        if(lt != rt && people[lt] + people[rt] <= limit) lt++;
        rt--;

        answer++;
    }

    return answer;
}
```

투 포인터를 사용하면 훨씬 간단해진다.

먼저 주어진 배열이 정렬된 상태여야 한다. 두 포인터가 가리키는 값의 합에 따라 처리 기준이 달라지기 때문이다. 두 포인터가 어긋날 때까지 아래 과정을 반복한다.

- 선택된 두 사람의 무게합이 `limit`보다 같거나 작으면 `answer++` 후 `lt`, `rt` 포인터 이동(`lt++`, `rt--`)
- 선택된 두 사람의 무게합이 `limit`보다 크면 `answer++` 후 `rt` 포인터만 이동(`rt--`)

배열이 정렬되어 있다는 가정 하에 단순 반복보다 더 빠른 속도로 결과를 얻을 수 있다. 두 포인터가 어긋나는 시점의 결과를 구하는 것 외에도 두 포인터가 가리키는 값의 조합이 원하는 값인지를 확인하는 경우에도 활용할 수 있다.