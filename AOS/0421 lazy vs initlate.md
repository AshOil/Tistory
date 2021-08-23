# 지연 초기화 `lazy` vs `lateinit`

> 프로젝트를 진행하다가 `lazy by` 와 `lateinit`이 종종 보이곤 했다. 애써 모른척 지나가려 했지만, 자꾸 눈에 밟히기 시작했다... 둘 다 변수 선언을 뒤로 미루는 느낌인거 같은데, `게으름(lazy)` 와 `지각(late)` 어느 녀석이 더 못난 녀석인지 한 번 알아보자!



## Why 지연초기화?

> 코틀린 언어에는 `null`값을 안정적으로 처리하기 위해 `null Safety`가 존재한다. `null`은 프로그래밍 하면서 항상 말썽꾸러기 역할을 담당하기 때문이다.
>
> 이러한 이유로 오류를 방지하기 위해 `Nullable`처리가 남발될 수 잇는데, 이를 방지하기 위해 `지연 초기화`를 도입했다.



## 1. lateinit

> 변수(프로퍼티)만 미리 선언하고 초기화(생성자 호출)을 나중에 하는 경우가 있는데, 이때 `lateinit`을 사용할 수 있다.

```kotlin
// nullable로 선언하는 일반적인 방식

class Person {
    var name: String? = null
    init {
        name = "Ashoil"
    }
    fun process() {
        name?.plus("kim")
        print("이름의 길이 = ${name?.length}")
        print("이름의 첫글자 = ${name?.substring(0.1)}")
    }
}
```

> 다음과 같이 `Safe Call(?.)`이 남용되어 가독성도 떨어지고 지저분해 보인다! 🤸‍♂️



```kotlin
// lateinit을 사용하는 경우

class Person {
    lateinit var name: String
    init {
        name = "Ashoil"
    }
    fun process() {
        name.plus("kim")
        print("이름의 길이 = ${name.length}")
        print("이름의 첫글자 = ${name.substring(0.1)}")
    }
}
```

> 훨씬 깔끔하고 가독성이 좋다!!



### lateinit의 특징

- var로 선언된 클래스의 프로퍼티에만 사용할 수 있다.
- null은 허용되지 않습니다.
- 기본 자료형 Int, Long, Double, Float 등은 사용할 수 없다.



### lateinit 주의사항

> `lateinit`은 변수를 선언만 해놓은 상태이기 때문에, 초기화 하지 않은 상태에서 프로퍼티를 참조하면 null 예외가 발생해 앱이 종료될 수 있습니다.





## 2. lazy

>`lazy`는 읽기전용 변수인 `val`을 사용하는 지연초기화입니다.
>
>`initlate`는 입력된 값을 변경할 수 있지만, `lazy`는 불가능하다.
>
>val로 변수 선언 후, 뒤에 `by lazy`를 붙이고 다음에 `중괄호({})`에 초기화할 값을 넣으면 된다.



```kotlin
class company {
    val person : Person by lazy {Person()}
    init {
        // lazy는 선언시 초기화를 하기 때문에 따로 초기화가 필요하지 않습니다.
    }
    fun process() {
        print("person의 이름은 ${person.name}")
    }
}
```



### lazy의 특징

- 따로 초기화가 필요하지 않다.
- 변수가 호출되는 시점에 `by lazy{}`안에 넣은 값으로 초기화 된다. 즉 process 매서드에서 person.name이 호출되는 순간 초기화 되는것!!
- by lazy를 사용하면 반환값의 타입을 추론할 수 있기 때문에, 따로 타입을 선언하지 않아도 된다.

```kotlin
val person by lazy{ person() }
```



### lazy 주의사항

> 지연초기화는 말그대로 최초 호출되는 시점에 초기화가 일어난다.  
>
> -> 초기화하는데 사용하는 리소스가 너무 크면 처리 속도에 영향을 미칠 수 있다.