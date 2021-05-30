# LiveData 활용하기

> 이번 프로젝트에서 `MVVM Model`을 활용하면서 `ViewModel`에서 `LiveData`를 활용해서 데이터를 처리하곤 했다. 그런 와중에?! API 통신을 통해서 불러온 데이터를 적용할 때, `scope` 범위를 넘어가서 제대로 처리 되지 않았다. 
>
> 그래서  공부하는 와중에 `setValue()`와 `postValue()`라는 편리한 친구들이 있다는 것을 알았다.
>
> [예전 글](https://ashoil.tistory.com/7)에도 LiveData에 대해 간략하게 적어놓은 부분이 있다.



## 1. [LiveData란](https://developer.android.com/topic/libraries/architecture/livedata?hl=ko)

> `LiveData`란 식별 가능한 데이터 홀더 클래스이다. LiveData는 수명 주기를 인식할 수 있기 때문에 활동 수명 주기 상태에 있는 구성요소 관찰차만 업데이트합니다. 
>
> (계속 관찰하고 있다가 값이 업데이트 되면 작동한다~~~ 대충 이런 느낌😛)



###  - Observer

> `Observer` 클래스로 표현되는 관찰자는 수명주기가 `STARTED` 나 `RESUME`이면 활동상태로 간주하고 업데이트 정보를 전달한다.



## 2. setValue()

> 말그대로 `value`를 설쟁해주는 함수이다.
>
> LiveData를 참조하고 있는 `Observer`가 있을 때, `setValue()`로 값이 업데이트 된다면, 그 값이 바로 반영되서 나타내준다.



## 3. postValue()

> `postValue()`는 네트워크 요청 또는 데이터베이스 로드 완료에 응답하는 등의 다양한 이유로 호출된 데이터를 업데이트하기 위해 호출될 수 있습니다.