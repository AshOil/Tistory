# CS - 2화. 선택 정렬(Selection Sort)

> `Selection Sort`는 넣을 위치를 정해놓고, 어떤 원소를 넣을지 찾아 떠나는 방식이다.
>
> 작은 걸 찾아 떠나는기? ,큰 걸 찾아 떠나는 가에 따라서 오름차순/내림차순이 결정된다.
>
> [bubble Sort](https://ashoil.tistory.com/16)와 혼동하는 경우가 있다! 





![다운로드 (1)](CS - 2화. 선택 정렬(Selection Sort).assets/다운로드 (1).gif)





- 첫번째 자리를 채워볼까? --> 누가 젤 작나~~ 이런 느낌
- 이젠 두번째!!  .....끝날때까지 반복



## 장/단점

- 장점
  - 코드가 간결하다. (알고리즘이 간단하다.)
  - 비교되는 횟수에 비해 실제 교환이 이뤄지는 숫자가 적다.
  - `별도의 메모리 공간`을 필요로하지 않는다.

- 단점
  - 시간복잡도가 모두 `O(N^2)`로 비효율적이다.
  - 불안정 정렬(Unstable Sort)이다.



#### 그래서 `안정 정렬`, `불안정 정렬`이 뭔데?

- 정렬의 `안정적 특성 `

  - 정렬되지 않은 상태에서 `같은 키값`을 가진 원소의 순서가 `정렬 후에도!!` 순서가 유지되느냐를 의미한다.

  - 만일 list = [5, 2, 4, 8, 4, 3] 이라 하자.

  - 이때 list를 정렬했을 때, `2번 idx의 4` 와 `4번 idx의 4`가 현재 순서를 유지할 수 있는가 에 대한 특성. 

  - 2번이 항상 4번보다 앞서서 위치한다 -> `안정 정렬`

    항상 그렇진 않다 -> `불안정 정렬`



## 코드

```python
def selectionSort(x):
    length = len(x)
    for i in range(length-1):
        min_idx =  i
        for j in range(i+1, length):
            if x[min_idx] > x[j]:
                min_idx = j
        x[i], x[min_idx] = x[min_idx], x[i]
        print(x)
    return x

x = [5, 7, 4, 2, 6, 8, 1, 3]

--- print ---
# 0번 idx에 뭘 넣어볼까? --> 0번 인덱스랑 바꿀사람..... 근데 0번이 젤 작아 pass
[1, 7, 4, 2, 6, 8, 5, 3]
# 다음 1번 idx 7... 4 ...2..... 2가 젤 작네! 2 이리콤! ... 이런식 반복
[1, 2, 4, 7, 6, 8, 5, 3]
[1, 2, 3, 7, 6, 8, 5, 4]
[1, 2, 3, 4, 6, 8, 5, 7]
[1, 2, 3, 4, 5, 8, 6, 7]
[1, 2, 3, 4, 5, 6, 8, 7]
[1, 2, 3, 4, 5, 6, 7, 8]
[1, 2, 3, 4, 5, 6, 7, 8]
```



## 시간 복잡도

- `O(N^2)`  : (n-1) + (n-2) + (n-3) + ... + 3 + 2 + 1 ==> n(n-1)/2

- 항상 모든 원소를 비교해야하기 때문에, 어떠한 케이스에도 상관없이 `동일한 시간복잡도`를 나타낸다

  (최악의 경우 == 최선의 경우 == 평균의 경우)



#### 참고 자료

https://godgod732.tistory.com/10

https://github.com/GimunLee/tech-refrigerator/blob/master/Algorithm/%EC%84%A0%ED%83%9D%20%EC%A0%95%EB%A0%AC%20(Selection%20Sort).md#%EC%84%A0%ED%83%9D-%EC%A0%95%EB%A0%AC-selection-sort

https://github.com/WooVictory/Ready-For-Tech-Interview/blob/master/Algorithm/%EC%84%A0%ED%83%9D%20%EC%A0%95%EB%A0%AC(Selection%20Sort).md

https://gaemi606.tistory.com/entry/%EA%B1%B0%ED%92%88%EC%A0%95%EB%A0%ACBubble-sort-%EC%84%A0%ED%83%9D%EC%A0%95%EB%A0%ACSelection-sort