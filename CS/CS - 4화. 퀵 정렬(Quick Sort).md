# CS - 4화. 퀵 정렬(Quick Sort)

> `Quick Sort`는 배열 중 하나의 원소를 `기준점(피벗: pivot)`으로 갖고, 그 기준점보다 큰것과 작은 것을 분류에서 넣어놓고 나중에 합치는 방식
>
> `quick`이라는 이름값처럼 다른 정렬보다 훨씬 빠르게 작동한다.



- 퀵 정렬은 `분할 정복 방식`을 통해 배열을 정렬한다.
  - `분할정복 방식` : 문제를 더 작은 문제로 분리하고, 그 분리한 결과들을 모아 원래의 결과를 도출한다.
    - `분할(Divide)` : `피벗`을 기준으로 비균등하게 2개의 부분 배열(기준보다 작은거 / 기준보다 큰거)로 분할한다.
    - `정복(Conquer)`: 부분 배열을 `정렬`한다. 부분 배열의 크기가 충분히 작지 않으면 `순환 호출` 을 이용하여 다시 분할 정복 방법을 적용한다. - `재귀`적 방식
    - `결합(Combine)`: 정렬된 부분 배열들을 하나의 배열에` 합병`한다.

  - 이때 재귀는 리스트의 크기가 0이나 1 될때까지 반복된다.



![quick_sort](CS - 4화. 퀵 정렬(Quick Sort).assets/quick_sort.gif)



- 노란색 바 = `피벗` 

- 초록색 바 = `less(피벗보다 작은경우)`

- 보라색 바 = `more(피벗보다 큰 경우)`

  

  



## 장/단점

- 장점
  - 속도가 빠르다.

    - `O(NlogN)`의 시간 복잡도를 갖는 다른 정렬알고리즘과 비교해도 빠른편에 속한다. WHY?

      1. 불필요한 데이터 이동 X
      2. 먼 거리의 데이터를 교환
      3. 한번 결정된 피벗들은 연산에서 제외

      

  - 추가 메모리 공간을 필요로 하지 않는다.

    - 퀵 정렬은 O(log n)만큼의 메모리를 필요로 한다.
      

- 단점

  - 불안정 정렬이다.
  - 정렬된 배열에 경우, 오히려 수행시간이 길어진다. (계속 재귀적으로 들어가야하기 때문에!)





## 코드

```python
def quickSort(x):
    if len(x) <= 1:
        return x

    pivot = x[len(x) // 2] # 중간의 값을 하나 기준으로 삼는다.
    less = []
    more = []
    equal = []
    for a in x:
        if a < pivot:
            less.append(a)
        elif a > pivot:
            more.append(a)
        else:
            equal.append(a)

    print(f"작은 + {less}")
    print(f"기준 + {equal}")
    print(f"큰 + {more}")
    print("--------------")
    return quickSort(less) + equal + 

x = [5, 7, 4, 2, 6, 8, 1, 3]

--- print ---

작은 + [5, 4, 2, 1, 3]
기준 + [6]  -> 8//2 --> 4번 idx가 기준이 됨!
큰 + [7, 8]
--------------
작은 + [1]
기준 + [2]
큰 + [5, 4, 3]
--------------
작은 + [3]
기준 + [4]
큰 + [5]
--------------
작은 + [7]
기준 + [8]
큰 + []
--------------
[1, 2, 3, 4, 5, 6, 7, 8]

Process finished with exit code 0

```



## 시간 복잡도

- 최선의 경우: `O(NlogN)` : 피벗값이 항상 중간인 경우!!

  - 반씩 잘라서 비교하고, 그에 따라 한꺼번에 정렬되는 케이스가 많음!

  

![img](CS - 4화. 퀵 정렬(Quick Sort).assets/quick-sort-002.png)



- 평균의 경우 : `O(NlogN)` 

- 최악의 경우 : `O(ㅜ^2) ` : 정렬이 되어 있을 때, 피벗을 앞에서 부터 잡게되면!!

  

```python
x = [1, 2, 3, 4, 5, 6]

------------------------
quickSort(x)  #x = [1, 2, 3, 4, 5, 6]
-> quickSort(less_1) + equal_1 + quickSort(more_1) # less_1 = [] equal_1 = [1] more_1 = [2,3,4,5,6]
-> quickSort(less_2) + equal_2 + quickSort(more_2) # less_2 = [] equal_2 = [2] more_2 = [3,4,5,6]
-> quickSort(less_3) + equal_3 + quickSort(more_3) # less_3 = [] equal_3 = [3] more_3 = [4,5,6]

# 이렇게 비효율적인 재귀가 계속해서 발생함!
```



![img](CS - 4화. 퀵 정렬(Quick Sort).assets/quick-sort-003.png)







#### 참고 자료

https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Algorithm/%EC%82%BD%EC%9E%85%20%EC%A0%95%EB%A0%AC(Insertion%20Sort).md

https://gaemi606.tistory.com/entry/%EA%B1%B0%ED%92%88%EC%A0%95%EB%A0%ACBubble-sort-%EC%84%A0%ED%83%9D%EC%A0%95%EB%A0%ACSelection-sort



