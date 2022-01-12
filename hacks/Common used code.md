### Kill app process
Kills the process, first put the app in the foreground, use the command on the terminal, and then launch the app from the emulator menu.

`adb shell am kill com.puntogris.myapplication`

### Test coroutines
If we dont do this we gonna get an error if we launch a coroutine from a viewModel for example as it runs on another thread or dispatcher

https://kotlin.github.io/kotlinx.coroutines/kotlinx-coroutines-test/

```kotlin
class SomeTest {

    private val testDispatcher = TestCoroutineDispatcher()
    
    @Before
    fun setUp() {
        Dispatchers.setMain(testDispatcher)
    }

    @After
    fun tearDown() {
        Dispatchers.resetMain() // reset the main dispatcher to the original Main dispatcher
        testDispatcher.cleanupTestCoroutines()
    }

    @Test
    fun testSomeUI() = runBlocking {
        launch(Dispatchers.Main) {  // Will be launched in the mainThreadSurrogate dispatcher
            // ...
        }
    }
}
```


### ViewModel assited inject Dagger2

#### Factory
```kotlin
class MyViewModelFactory @AssistedInject constructor(  
    private val repo: HomeRepository,  
    @Assisted owner: SavedStateRegistryOwner  
) : AbstractSavedStateViewModelFactory(owner, null) {  
    override fun <T : ViewModel?> create(  
        key: String,  
        modelClass: Class<T>,  
        handle: SavedStateHandle  
    ): T = HomeViewModel(repo, handle) as T  
}  

@AssistedFactory  
interface MyViewModelAssistedFactory {  
    fun create(owner: SavedStateRegistryOwner): MyViewModelFactory  
}
```

#### Create ViewModel
```kotlin
@Inject  
lateinit var factory: MyViewModelAssistedFactory  
private val viewModel: HomeViewModel by viewModels { factory.create(this) }

//Another way

@Inject
lateinit var assistedFactory: MyViewModelAssistedFactory
private lateinit var viewModel: MyViewModel

//onCreteView
val viewModelFactory = assistedFactory.create(this)     
viewModel = ViewModelProvider(this, viewModelFactory).get(MyViewModel::class.java)
```


### Binding

```kotlin
private var _binding: ScreenBinding? = null
private val binding get() = _binding!!

//onCreateView, setup the binding
_binding = DataBindingUtil.inflate(inflater, layout, container, false)

//onDestroyView, after super call
_binding = null
    
```

### FragmentContainerView

#### Activity
```kotlin
val navController = 
    (supportFragmentManager.findFragmentById(R.id.nav_host_fragment) as NavHostFragment).navController
```

#### View
```xml
<androidx.fragment.app.FragmentContainerView  
 android:id="@+id/nav_host_fragment"  
 android:name="androidx.navigation.fragment.NavHostFragment"  
 android:layout_width="match_parent"  
 android:layout_height="match_parent"  
 app:defaultNavHost="true"  
 app:navGraph="@navigation/navigation" />
```

### ViewHolder

```kotlin
class ItemViewHolder(private val binding: ItemVhBinding) : RecyclerView.ViewHolder(binding.root) {  

    fun bind(item: Item) {  
        binding.item = item
        binding.executePendingBindings()  
    }  
    companion object {  
        fun from(parent: ViewGroup): ItemViewHolder{  
            val inflater = LayoutInflater.from(parent.context)  
            val binding = ItemVhBinding.inflate(inflater, parent, false)  
            return ItemViewHolder(binding)  
        } 
    }
}
```

### Livedata gerOrAwaitValue

https://github.com/android/architecture-components-samples/blob/85587900b68a5d3a7edf95065fe2d8c768e66164/GithubBrowserSample/app/src/test-common/java/com/android/example/github/util/LiveDataTestUtil.kt

```kotlin
fun <T> LiveData<T>.getOrAwaitValue(
    time: Long = 2,
    timeUnit: TimeUnit = TimeUnit.SECONDS,
    afterObserve: () -> Unit = {}
): T {

    var data: T? = null
    val latch = CountDownLatch(1)
    val observer = object : Observer<T> {

        override fun onChanged(o: T?) {
            data = o
            latch.countDown()
            this@getOrAwaitValue.removeObserver(this)
        }
    }

    this.observeForever(observer)
    afterObserve.invoke()

    // Don't wait indefinitely if the LiveData is not set.

    if (!latch.await(time, timeUnit)) {
        this.removeObserver(observer)
        throw TimeoutException("LiveData value was never set.")
    }

    @Suppress("UNCHECKED_CAST")
    return data as T
}
```

### Flow
```kotlin
// Take the second item
outputFlow.drop(1).first()
// Take the first 5 items
outputFlow.take(5).toList()
// Take the first 5 distinct items
outputFlow.take(5).toSet()
// Takes the first item verifying that the flow is closed after that
outputFlow.single()
```