# CS - 5화. 병합 정렬(Merge Sort)

> `Merge Sort`는   `Quick Sort`과 같이 `분할 정복 방식`을 통해 정렬이 이루어진다

- `분할정복 방식` : 문제를 더 작은 문제로 분리하고, 그 분리한 결과들을 모아 원래의 결과를 도출한다.

  - `분할(Divide)` : `피벗`을 기준으로 비균등하게 2개의 부분 배열(기준보다 작은거 / 기준보다 큰거)로 분할한다.
  - `정복(Conquer)`: 부분 배열을 `정렬`한다. 부분 배열의 크기가 충분히 작지 않으면 `순환 호출` 을 이용하여 다시 분할 정복 방법을 적용한다. - `재귀`적 방식
  - `결합(Combine)`: 정렬된 부분 배열들을 하나의 배열에` 합병`한다.
  - len()이 2보다 작으면 return 한다.

  


- Merge Sort  vs.  Quick Sort
  - 퀵 정렬 :  `Pivot`을 통해 정렬 -> 영역을 자른다.
  - 합병 정렬 : 영역을 자를 수 있을 만큼 자른다 -> 정렬한다





![Merge Sort](CS - 5화. 병합 정렬(Merge Sort).assets/Merge Sort.gif)





## 장/단점

- 장점

  - 속도가 일정하다.
    - 데이터의 분포에 영향이 적다. 즉 입력데이터에 크게 상관없이 정렬되는 시간이 O(NlogB)으로 동일하다.
  - 데이터가 매우 큰 경우, `LinkedList`를 사용한다면 어떠한 정렬보다 효율적이다!

  - 안정 정렬이다.

  

- 단점

  - 추가적인 메로리를 필요로 한다.
    - 레코드를 배열로 구성 한 경우
    - 메모리 낭비, 제자리 정렬 X

  - 레코드 크기가 큰 경우, 이동횟수가 많다. -> 시간 낭비 ㅠ.ㅠ



## 코드

```python
def merge_sort(arr):
    if len(arr) < 2:
        return arr

    mid = len(arr) // 2
    # 이때 slice를 사용하는 건 코드상 깔끔해지지만
    # list의 복사가 일어나기 때문에 메모리 효율은 떨어질 수 있다.
    low_arr = merge_sort(arr[:mid])  
    high_arr = merge_sort(arr[mid:])

    merged_arr = []
    l = h = 0
    # 줄세워 놓은거 0번부터 시작
    while l < len(low_arr) and h < len(high_arr):
        # 시작부터 하나씩 비교해서 더 작은거 merge_arr에 넣고, 한칸 앞으로
        if low_arr[l] < high_arr[h]:
            merged_arr.append(low_arr[l])
            l += 1
        else:
            merged_arr.append(high_arr[h])
            h += 1
    # 하나가 끝났으면, 나머지 그냥 넣어버리기
    merged_arr += low_arr[l:]
    merged_arr += high_arr[h:]
    print(merged_arr)
    return merged_arr

x = [5, 7, 4, 2, 6, 8, 1, 3]

--- print ---

[5, 7]
[2, 4]
[2, 4, 5, 7]
[6, 8]
[1, 3]
[1, 3, 6, 8]
[1, 2, 3, 4, 5, 6, 7, 8]

```



## 시간 복잡도

- 모든 경우에서 `O(NlogN)`의 시간복잡도를 나타낸다.
  - 값을 비교하는 상황에서 `N`개 모두 비교
  - 반씩 자르기 때문에, 반복하는 케이스의 경우가 계속 반씩 줄어든다(logN)



## 개선된 코드!!

- 위 작성된 코드는 계속해서 새로운 배열을 생성하고 리턴하기 때문에 `불필요한 메모리 사용`이 많다.
- 인덱스로 접근해 업데이트 하면 메모리 사용을 대폭 줄일 수 있다.(`In-place sort`)

```python
def merge_sort(arr):
    def sort(low, high):
        if high - low < 2:
            return
        mid = (low + high) // 2
        sort(low, mid)
        sort(mid, high)
        merge(low, mid, high)

    def merge(low, mid, high):
        temp = []
        l, h = low, mid

        while l < mid and h < high:
            if arr[l] < arr[h]:
                temp.append(arr[l])
                l += 1
            else:
                temp.append(arr[h])
                h += 1

        while l < mid:
            temp.append(arr[l])
            l += 1
        while h < high:
            temp.append(arr[h])
            h += 1

        for i in range(low, high):
            arr[i] = temp[i - low]
        print(x)
    return sort(0, len(arr))

x = [5, 7, 4, 2, 6, 8, 1, 3]

----------------------------------

[5, 7, 4, 2, 6, 8, 1, 3]
[5, 7, 2, 4, 6, 8, 1, 3]
[2, 4, 5, 7, 6, 8, 1, 3]
[2, 4, 5, 7, 6, 8, 1, 3]
[2, 4, 5, 7, 6, 8, 1, 3]
[2, 4, 5, 7, 1, 3, 6, 8]
[1, 2, 3, 4, 5, 6, 7, 8]
```



#### 참고 자료

https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Algorithm/%EB%B3%91%ED%95%A9%20%EC%A0%95%EB%A0%AC(Merge%20Sort).md

https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/MergeSort.md

https://www.daleseo.com/sort-merge/



