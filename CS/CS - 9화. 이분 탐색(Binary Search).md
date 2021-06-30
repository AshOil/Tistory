# CS - 9화. 이분 탐색(Binary Search)

> `Binary Search`는 말 그대로 탐색할 것으 반 씩 잘라서(이분해서) 찾아가는 방식 



## 작동 방식

1. 일단 배열을 정렬해준다.
2. `left`, `right` 를 통해 `mid`값을 지정해준다.
3. 현재 내가 찾으려는 값과 `mid`값을 비교하고, 값이 더 작다면 왼쪽편, 크다면 오른쪽편





![Binary Vs Linear Search Through Animated Gifs | Penjee, Learn to Code](CS - 9화. 이분 탐색(Binary Search).assets/binary-and-linear-search-animations.gif)





## 코드

```python
def binarySearch(array, value, low, high):
	if low > high:
		return False
	mid = (low+high) / 2
	if array[mid] > value:
		return binarySearch(array, value, low, mid-1)
	elif array[mid] < value:
		return binarySearch(array, value, mid+1, high)
	else:
		return mid
```





## 시간 복잡도

- 일반적인 전체 탐색 : `O(N)`
- `이분탐색` : `O(logN)`





#### 참고 자료

https://bowbowbow.tistory.com/8

https://www.codesdope.com/course/algorithms-count-and-sort/



