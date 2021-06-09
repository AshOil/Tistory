# CS - 7화. 기수정렬(Radix Sort)

> `Radix Sort`는 서로 비교하는 것 없이 `기수`별로 정렬하는 알고리즘 형태        ~~몇기냐?~~ 
>
> 간단히 생각하면 각 자리수끼리 비교해서 정렬을 하는 형태



## LSD vs. MSD

- LSD는 낮은 자리수부터 비교하면서 정렬하는 것이고, MSD는 높은 자리수부터 비교하면서 정렬하는 것

- `LSD`

  - 짧은 것이 긴것보다 먼저 나오고, 같은 길이라면 사전순으로 정렬된다.
  - 일반적으로 안정정렬이다.

- `MSD`

  - `문자열`이나 `고정길이 정수 표현` 정렬에 적합

  - 일반적인 숫자를 정렬할 경우:  **[1, 10, 2, 3, 4, 5, 6, 7, 8, 9]** 이런식으로 정렬됨

  - 불안정정렬로 순서가 유지되지 않을 수 있다.

    



![기수정렬(Ridix Sort)](CS - 7화. 기수 정렬(Radix Sort).assets/img.gif)





## 코드

```python
# 좀더 공부가 필요할 듯 합니다. 우선 개념적으로 접근하겠습니다. ㅠ.ㅠ

def radix_sort(num):
    # 최대 digit을 알아보기 위해 가장 큰 수를 찾는다
    max1 = max(num)
    exp = 1
    while max1 / exp > 0:
        count_sort(num, exp)
        exp *= 10

def count_sort(A, k):
    B = [0] * len(A)
    C = [0] * (10)  # 1의 자리, 10의 자리수만 비교하기 때문에 범위는 0~9이다

    for i in range(0, len(A)):  # 각 element가 몇개있는지 C에 저장한다
        index = (A[i] // k)
        C[(index) % 10] += 1

    for i in range(1, 10):  # C를 누적값으로 바꾼다, 0~9까지 밖에 없다
        C[i] += C[i - 1]

    i = len(A) - 1
    while i >= 0:  # C 를 indexing해서 정렬된 리스트를 찾는다
        index = (A[i] // k)
        B[C[(index) % 10] - 1] = A[i]
        C[(index) % 10] -= 1
        i -= 1

    # 기존 리스트에 복사를 한다
    for i in range(len(A)):
        A[i] = B[i]


x = [5, 7, 4, 2, 6, 8, 1, 3]
```



## 장/단점

- 장점
  - 문자열과 정수 둘 다 정렬이 가능하다.
- 단점
  - 자릿수가 없는 것은 정렬이 불가능하다.  ex) 부동소숫점
  - 중간 데이터를 저장할 공간이 필요하다.





## 시간 복잡도

-  `O(kn)`의 시간복잡도를 나타낸다.
  - 여기서 k는 가장 큰 자릿수를 나타낸다.





#### 참고 자료

https://devjin-blog.com/sort-algorithm-9/

https://github.com/gyoogle/tech-interview-for-developer/blob/master/Algorithm/Sort_Radix.md



