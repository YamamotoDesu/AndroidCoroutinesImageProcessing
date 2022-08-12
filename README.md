# AndroidCoroutinesImageProcessing

![2022-08-12 15 36 19](https://user-images.githubusercontent.com/47273077/184298186-25bdd5b0-ef79-4176-9f18-c6275c5bae2f.gif)

MainActivity
```kt

class MainActivity : AppCompatActivity() {

    private val IMAGE_URL = "https://raw.githubusercontent.com/DevTides/JetpackDogsApp/master/app/src/main/res/drawable/dog.png"
    private val coroutineScope = CoroutineScope(Dispatchers.Main)

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        coroutineScope.launch {
            val originalDeferred = coroutineScope.async(Dispatchers.IO) { getOriginalBitmap() }

            val originalBitmap = originalDeferred.await()

            loadImage(originalBitmap)
        }
    }

    private fun getOriginalBitmap() =
        URL(IMAGE_URL).openStream().use {
            BitmapFactory.decodeStream(it)
        }

    private fun loadImage(bmp: Bitmap) {
        progressBar.visibility = View.GONE
        imageView.setImageBitmap(bmp)
        imageView.visibility = View.VISIBLE
    }
}
```
