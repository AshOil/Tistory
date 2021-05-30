# Url을 통해 image불러오고 bitmap으로 변경하기!?



## 1. Class 파일 만들기!

```kotlin
class URLtoBitmap() : AsyncTask<Void, Void, Bitmap>() {
    lateinit var url: URL
    override fun doInBackground(vararg params: Void?): Bitmap {
        val bitmap = BitmapFactory.decodeStream(url.openStream())
        return bitmap
    }
    override fun onPreExecute() {
        super.onPreExecute()

    }
    override fun onPostExecute(result: Bitmap) {
        super.onPostExecute(result)
    }
}
```





## 2.  사용할 곳에서 쓰기

```kotlin
var image_task: URLtoBitmapTask = URLtoBitmapTask()
image_task = URLtoBitmapTask().apply {
    url = URL(item[position].thumbnailPath)
}
var bitmap: Bitmap = image_task.execute().get()
```



## 3. Bitmap  회전 시키는 함수 생성

```kotlin
fun Bitmap.rotate(degrees: Float): Bitmap {
    val matrix = Matrix().apply { postRotate(degrees) }
    return Bitmap.createBitmap(this, 0, 0, width, height, matrix, true)
}
```





## 4. 원하는 곳에 적용!

```kotlin
IMAGEVIEW.setImageBitmap(bitmap.rotate(90f))
```

