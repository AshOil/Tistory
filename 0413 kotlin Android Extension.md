# Kotlin Android Extension

> 기존 `Java`에서는 `.xml`를 `id`로  참조할 때, 복잡한 과정을 거쳐야 했다. 😥
>
> 하지만 우리 `Kotlin`과 함께라면 더 이상 복잡한 과정은 그만!! 코딩 멈춰!! 🖐



- `Kotlin Android Extension`란?

  > 기존 안드로이드 개빌 시 XML 뷰 컴포넌트를 다루기 위해서 귀찮고 복잡하게 선언한 `findViewById()`나 `ButterKnife` 라이브러리 등을 사용했어야 했다.
  >
  > 하지만 `Kotlin`에서 공식적으로 지원하는 [KTX](https://developers-kr.googleblog.com/2018/02/introducing-android-ktx-even-sweeter-kotlin-development-for-android.html) 를이용해 뷰 컴포넌트를 간단하게 처리할 수 있다.



### 1. build.gradle

```
plugins {
    ...
    id 'kotlin-android-extensions'
    ...
}
```



### 2. res/layout/activity_main.xml

```
    <androidx.viewpager2.widget.ViewPager2
    
    	// 요렇게 아이디 작성!
        android:id="@+id/viewPager_idol"
        
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
```



### 3. MainActivity.kt

```kotlin
...
// 이렇게 불러오기!!
import kotlinx.android.synthetic.main.activity_main.*
...

class MainActivity : AppCompatActivity() {
	
    // 요렇게 직접적으로 viewPager_idol에 접근할 수 있다!
    viewPager_idol.adapter = ViewPagerAdapter(getIdolList()) // 
    viewPager_idol.orientation = ViewPager2.ORIENTATION_VERTICAL // 방향을 가로로

}
```

