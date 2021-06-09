# CS - 6화. 힙정렬(Heap Sort)

> `Heap Sort`는 말그대로 `Heap(힙)`을 이용한 정렬방식
>
> **다시 최대 힙을 구성할 때까지** 부모 노드와 자식 노드를 swap하며 재귀 진행
>
> `퀵정렬`과 `병합정렬`의 성능이 좋기 때문에 `힙 정렬`의 사용빈도가 높지는 않음.



## `힙(heap)`이란?

- `완전 이진 트리`의 일종, 우선순위 큐를 위해 만들어진 자료구조 형태
- 여러개의 값 중, 최대 혹은 최솟값을 빠르게 찾기 위한 구조
- 힙은 `반정렬상태(느슨한 정렬상태)`이다.
  - 이때, 느슨한 정렬상태란? 
    - 큰 값이 상위에 있고, 낮은 값이 하위에 있다는 정도
    - 부모 노드의 키값이 자식 노드의 키값보다 항상 크다(작다). 
    - 동등한 노드 간 대소관계는 알 수 없다.
- 일반적인 `이진 탐색 트리`에서는 중복값을 허용하지 않지만 힙트리에선 가능하다.





![image-20210607134235350](CS - 6화. 힙 정렬(Heap Sort).assets/image-20210607134235350.png)



## 일반적인 힙의 구현

- 힙의 자료구조는 `배열`이다.
- 편의상 0번 인덱스는 사용하지 않는다.
- 특정 위치의 노드번호는 항상 일정하다.
  - 새로운 노드가 추가되어도 변하지 않는다.
- `부모노드`와 `자식노드` 간  관계
  - 왼쪽 자식 idx = 부모 idx*2
  - 오른쪽 자식 idx = 부모 idx*2 + 1
  - 부모인덱스 = 자식 idx // 2







![img](CS - 6화. 힙 정렬(Heap Sort).assets/img.gif)



## 코드

```python
def heap_sort(arr):
    # 최대 힙 만들기
    for i in range(1, len(arr)):
        c = i
        while c:
            p = (c-1) // 2
            if arr[p] < arr[c]:
                arr[p], arr[c] = arr[c], arr[p]
            c = p

    # 힙 만들기
    for j in range(len(arr)-1, -1, -1):
        arr[0], arr[j] = arr[j], arr[0]
        p = 0
        c = 1
        while c < j:
            c = 2*p + 1
            if c < j - 1 and arr[c] < arr[c+1]:
                c += 1
            if c < j and arr[p] < arr[c]:
                arr[p], arr[c] = arr[c], arr[p]
            p = c
            print(arr)


x = [5, 7, 4, 2, 6, 8, 1, 3]
```



## 시간 복잡도

- 모든 경우에서 `O(NlogN)`의 시간복잡도를 나타낸다.





#### 참고 자료

https://gmlwjd9405.github.io/2018/05/10/data-structure-heap.html

https://gyoogle.dev/blog/algorithm/Heap%20Sort.html

https://www.daleseo.com/sort-merge/



