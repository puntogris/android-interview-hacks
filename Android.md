### App components

App components are the essential building blocks of an Android app. Each component is an entry point through which the system or a user can enter your app. Some components depend on others.

There are four different types of app components:

##### Activities
An _Activity_ is the entry point for interacting with the user. It represents a single screen with a user interface.

**Lifecycle:** 
 - onCreate: fires when the system first creates the activity. 
 - onStart: makes the activity visible to the user
 - onResume: this is the state in which the app interacts with the user
 - onPause: the system calls this method as the first indication that the user is leaving your activity
 - onStop: when your activity is no longer visible to the user
 - onDestroy:  is called before the activity is destroyed

##### Services
A _Service_ is a general-purpose entry point for keeping an app running in the background for all kinds of reasons.
 - Started service tell the system to keep them running until their work is completed. Ex: Music on the background.
 - Bound services run because some other app (or the system) has said that it wants to make use of the service.

**IntentService**
The Service runs on the UI thread while an IntentService runs on a separate worker thread.

When you want to perform multiple background tasks one by one which exists beyond the scope of an Activity then the `IntentService` is perfect.

The three primary features of an `IntentService` are:

- the background thread
- the automatic queuing of `Intent`s delivered to `onStartCommand()`, so if one `Intent` is being processed by `onHandleIntent()` on the background thread, other commands queue up waiting their turn
    
- the automatic shutdown of the `IntentService`, via a call to `stopSelf()`, once the queue is empty

**JobScheduler**

The **JobScheduler** API batches the similar work requests together and executes them based on available resources, specified condition, or interval. 

This is an API for scheduling various types of jobs against the framework that will be executed in your application's own process.
Is a system service that is used to schedule, execute, and if necessary cancel, jobs on behalf of an Android application.

##### Broadcast receivers
A _Broadcast receiver_ is a component that enables the system to deliver events to the app outside of a regular user flow, allowing the app to respond to system-wide broadcast announcements.

**LocalBroadcastManager**

If the communication is not between different applications on the Android device then is it suggested not to use the Global BroadcastManager because there can be some security holes while using Global Broadcastmanager and you don’t have to worry about this if you are using LocalBroadcastManager.LocalBroadcastManager is used to register and send a broadcast of intents to local objects in your process. It has lots of advantages:

 - You broadcasting data will not leave your app. So, if there is some leakage in your app then you need not worry about that.
 - Another thing that can be noted here is that other applications can’t send any kind of broadcasts to your app. So, you need not worry about security holes.

##### Content providers
A _Content provider_ component supplies data from one application to others on request. They serves the purpose of a relational database to store the data of applications.

#### Activating components
Three of the four component types—activities, services, and broadcast receivers—are activated by an asynchronous message called an _intent_. Intents bind individual components to each other at runtime. You can think of them as the messengers that request an action from other components, whether the component belongs to your app or another.

For activities and services, an intent defines the action to perform (for example, to _view_ or _send_ something) and may specify the URI of the data to act on, among other things that the component being started might need to know.

For broadcast receivers, the intent simply defines the announcement being broadcast. For example, a broadcast to indicate the device battery is low includes only a known action string that indicates _battery is low_.

Unlike activities, services, and broadcast receivers, content providers are not activated by intents. Rather, they are activated when targeted by a request from a ContentResolver.

### Intents
An Intent is a messaging object you can use to request an action from another app component.
 - Explicit Intents: For communication between the components of your application (we know the class name / address).
 - Implicit Intents: They must include enough information for the system to determine which of the available components is best to run for that intent.

#### Intent filter
An intent filter is an expression in an app's manifest file that specifies the type of intents that the component would like to receive.

When you create an implicit intent, the Android system finds the appropriate component to start by comparing the contents of the intent to the intent filters declared in the manifest file of other apps on the device. If the intent matches an intent filter, the system starts that component and delivers it the Intent object.

#### Sticky Intent
Sticky Intents allows communication between a function and a service. sendStickyBroadcast() performs a sendBroadcast(Intent) known as sticky, i.e. the Intent you are sending stays around after the broadcast is complete, so that others can quickly retrieve that data through the return value of registerReceiver(BroadcastReceiver, IntentFilter).

For example, if you take an intent for ACTION_BATTERY_CHANGED to get battery change events: When you call registerReceiver() for that action — even with a null BroadcastReceiver — you get the Intent that was last Broadcast for that action. Hence, you can use this to find the state of the battery without necessarily registering for all future state changes in the battery.

#### Pending Intent
If you want someone to perform any Intent operation at future point of time on behalf of you, then we will use Pending Intent.

### Manifest
The manifest file is an important part of our app because it defines the structure and metadata of our application, its components, and its requirements.

The manifest does a number of things in addition to declaring the app's components, such as the following:

- Identifies any user permissions the app requires, such as Internet access or read-access to the user's contacts.
- Declares the minimum API Level required by the app, based on which APIs the app uses.
- Declares hardware and software features used or required by the app, such as a camera, bluetooth services, or a multitouch screen.
- Declares API libraries the app needs to be linked against (other than the Android framework APIs), such as the Google Maps library.

### Application
The Application class in Android is the base class within an Android app that contains all other components such as activities and services. The Application class, or any subclass of the Application class, is instantiated before any other class when the process for your application/package is created.

### Context
Interface to global information about an application environment. This is an abstract class whose implementation is provided by the Android system. It allows access to application-specific resources and classes, as well as up-calls for application-level operations such as launching activities, broadcasting and receiving intents, etc.

You can understand very well, now, why the name is Context. It’s because it’s just that. The Context provides the link or hook, if you will, for an Activity, Service, or any other component, thereby linking it to the system, enabling access to the global application environment. In other words: the Context provides the answer to the components question of “where the hell am I in relation to app generally and how do I access/communicate with the rest of the app?”

### onSavedInstanceState() and onRestoreInstanceState() in activity
- `onSavedInstanceState()` - This method is used to store data before pausing the activity.
- `onRestoreInstanceState()` - This method is used to recover the saved state of an activity when the activity is recreated after destruction. So, the onRestoreInstanceState() receive the bundle that contains the instance state information.

### Activity launch mode

#### Standard
This is the default launch mode of activity (If not specified). It launches a new instance of an activity in the task from which it was launched. Numerous instances of the activity can be generated, and multiple instances of the activity can be assigned to the same or separate tasks. In other words, you can create the same activity multiple times in the same task as well as in different tasks.

####  Single Task
In this method of operation, a new task is always generated, and a new instance is added to the task as the root one. If the activity already exists on another task, no new instance is created, and the Android system transmits the intent information via the onNewIntent() function. At any one time, there will be just one instance of the activity.

#### Single Top
If an instance of the activity already exists at the top of the current task in this launch mode, no new instance will be generated, and the Android system will send the intent data through onNewIntent (). If an instance does not exist on top of the task, a new instance will be generated. You can use this launch mode to generate numerous instances of the same activity within the same task or across tasks, but only if the identical instance does not already exist at the top of the stack.

#### Single Instance
This is a highly unique start option that is only used in programs with a single activity. It works similarly to **Single Task**, except that no additional activities are generated in the same task. Any further activity initiated from this point will result in the creation of a new task.

### Fragment
A Fragment represent another screen inside the activity, a sub-activity.
A Fragment represents a reusable portion of your app's UI. 
A Fragment is a piece of an activity which enable more modular activity design. It's kind of a sub-activity.
A Fragment defines and manages its own layout, has its own lifecycle, and can handle its own input events. Fragments cannot live on their own--they must be _hosted_ by an activity or another fragment. The fragment’s view hierarchy becomes part of, or _attaches to_, the host’s view hierarchy.


When fragment come up on the screen:

 - onAttach : This method called first, To know that our fragment has been attached to an activity. We are passing the Activity that will host our fragment.
 - onCreate:  when a fragment instance initializes, just after the onAttach where fragment attaches to the host activity.
 - onCreateView: when it’s time for the fragment to draw its user interface for the first time. To draw a UI for your fragment, you must return a View component from this method that is the root of your fragment’s layout. You can return null if the fragment does not provide a UI.
 - onActivityCreated: when Activity completes its onCreate() method
 - onStart:  when a fragment is visible.
 - onResume: when a fragment is visible and allowing the user to interact with it. Fragment resumes only after activity resumes.

When fragment goes out off the screen:

 - onPause:  when a fragment is not allowing the user to interact; the fragment will get change with other fragment or it gets removed from activity or fragment’s activity called a pause.
 - onStop:   when the fragment is no longer visible; the fragment will get change with other fragment or it gets removed from activity or fragment’s activity called stop.
 - onDestroyView:  when the view and related resources created in onCreateView() are removed from the activity’s view hierarchy and destroyed.
 - onDestroy: when the fragment does its final clean up.
 - onDetach: when the fragment is detached from its host activity.

 #### When should you use a Fragment rather than an Activity?
  - When you have some UI components to be used across various activities
  - When multiple view can be displayed side by side just like viewPager

### Difference Between a Fragment and an Activity in Android

**An Activity** is a user interface component that is mainly used to construct a single screen of the application and represents the main focus of attention on a screen. An activity can host one or more fragments at a time. **Fragments**, as tablets emerged with larger screens, are reusable components that are attached to and displayed within activities. It is basically a piece of an activity that enables more modular activity design. We can call a fragment is a kind of sub-activity. It is always hosted by an activity. It has its own layout and its own behavior with its own life cycle callbacks. We can add or remove fragments in an activity while the activity is running. It is possible to develop a UI only using Activities, but this is generally a bad idea since their code cannot later be reused within other Activities, and cannot support multiple screens. 

**Activity** is the UI of an application through which user can interact and Fragment is the part of the Activity, it is a sub-Activity inside activity which has its own Life Cycle which runs parallel to the Activities Life Cycle.

---
 
We need to mention all activity it in the manifest.xml file 

Fragment is not required to mention in  the manifest file

---
  
We can’t create multi-screen UI without using fragment in an activity,

After using multiple fragments in a single activity, we can create a multi-screen UI.

---

Activity can exist without a Fragment  

Fragment cannot be used without an Activity.

---
Activity is not lite weight. 

The fragment is the lite weight.

### What is a retained Fragment?
By default, Fragments are destroyed and recreated along with their parent Activity’s when a configuration change occurs. Calling setRetainInstance(true) allows us to bypass this destroy-and-recreate cycle, signaling the system to retain the current instance of the fragment when the activity is recreated.

### View
The view is the component which Android provides us to design the layouts of the app. So, we can understand view as a rectangular area which is going to contain some element inside it.

A _View_ is a superclass for all the UI components.

Invisible vs Gone:

 - View.GONE: This view is invisible, and it doesn't take any space for layout purposes.
 - View.INVISIBLE: This view is invisible, but it still takes up space for layout purposes.

### What are ViewGroups and how they are different from the Views?
 - View objects are the basic building blocks of User Interface(UI) elements in Android. View is a simple rectangle box which responds to the user’s actions. Examples are EditText, Button, CheckBox etc. View refers to the android.view.View class, which is the base class of all UI classes.
 - ViewGroup is the invisible container. It holds View and ViewGroup. For example, LinearLayout is the ViewGroup that contains Button(View), and other Layouts also. ViewGroup is the base class for Layouts.


### What are Canvas API?

Canvas API in Android is a drawing framework which helps us to draw custom design like line, circle or even a rectangle. Using these we can make any shape whichever we want according to design.

The drawing of canvas happens in Bitmap, where we draw the outline and then the Paint API helps to fill color and whatever style we need

### Surface View
Provides a dedicated drawing surface embedded inside of a view hierarchy. You can control the format of this surface and, if you like, its size; the SurfaceView takes care of placing the surface at the correct location on the screen.

A SurfaceView is a custom view in Android that can be used to drawn inside it.  
  
The main difference between a View and a SurfaceView is that a View is drawn in the UI Thread, which is used for all the user interaction.  
  
If you want to update the UI rapidly enough and render a good amount of information in it, a SurfaceView is a better choice.

Gives more control over the timing to update it. In normal view we need to call invalidate or postInvalid, however it wont update inmediately but wait to the next VSCYNC event( 60 fps, every 16ms). In SurfaceView we can set any timing we want.

### Constraint Layout
ConstraintLayout combines a simple, expressive and flexible layout system with the powerful features built into the Android Studio Designer tool. It makes it easier to create responsive user interface layouts that adapt automatically to different screen sizes and changing device orientations.

#### Why did we need ConstraintLayout?

It make handling complex screen designs easier. It also improves the performance of complex layouts.  

With ConstraintLayout, even complex screen designs with nested layouts can be fast.

ConstraintLayout provides a level of flexibility that allows many of the features of older layouts to be achieved with a single layout instance. Before, you needed to nest multiple layouts.

This has the benefit of avoiding many problems inherent in nesting layouts. It allows designing so-called _flat_ or _shallow_ layout hierarchies. This leads to less complex layouts and improved user interface rendering performance at runtime.

ConstraintLayout is also implemented with an eye toward addressing the wide range of Android device screen sizes available on the market today.

The flexibility of ConstraintLayout makes it easier for user interfaces to be designed that respond and adapt to the device on which the app is running.

### ListView and RecyclerView

RecyclerView is a ViewGroup, which populates a list on a collection of data provided with the help of ViewHolder and draws it to the user on-screen.

The major components of RecyclerView are,
- Adapter:  It takes the data set which has to be displayed to the user in RecyclerView. It is like the main responsible class to bind the views and display it.
- ViewHolder : Is a type of a helper class that helps us to draw the UI for individual items that we want to draw on the screen.
- LayoutManager: LayoutManager in recyclerView helps us to figure out how we need to display the items on the screen.

#### ViewHolder
The ViewHolder pattern is entirely optional in ListView, but it’s baked into RecyclerView. Making it more flexible but introducing a lot of boilerplate.

The ViewHolder pattern allows us to make our list scrolling act smoothly. It stores list row views references and, thanks to this, calling the `findViewById()` method only occurs a couple of times, rather than for the entire dataset and on each bind view.

#### LayoutManager
ListView only supports vertical scrolling, but RecyclerView isn’t limited to vertically scrolling lists.
Supports Linear, Grid and Staggered Layouts

#### Notifying adapter

We have a couple of cool notifiers on the RecyclerView’s adapter. We are still able to use `notifyDataSetChanged()` but there are also ones for particular list elements, like `notifyItemInserted()`, `notifyItemRemoved()` or even `notifyItemChanged()` and more. We should use the most appropriate ones for what is happening, so the proper animations will fire correctly.

#### ItemAnimator
As we can expect, it’s handling row views animations like list appearance and disappearance, adding or removing particular views and so on.

---
So, to conclude, RecyclerView is a more flexible control for handling "list data" that follows patterns of delegation of concerns and leaves for itself only one task - recycling items.

#### RecyclerView Performance

##### Use Image-Loading Library

As the Garbage Collection(GC) runs on the main thread, one of the reasons for unresponsive UI is **the continuous allocation and deallocation of memory,** which leads to the very frequent GC run. By using the bitmap pool concept, we can avoid it.

If we do not set the correct image width and height prior, the UI will **flicker** during the transition of loading(downloading of image) and setting of the image into the ImageView(actually making it visible when downloading completes).

##### Use Notify Item RecyclerView API

Whenever we have the use-case of the removal, the updation, the addition of item, use the Notify Item API.

Using `notifyItemRemoved()`, `notifyItemChanged()`, `notifyItemInserted()`, `notifyItemRangeInserted()`

##### setHasFixedSize()

RecyclerView size changes every time you add something no matter what. What setHasFixedSize does is that it makes sure (by user input) that this change of size of RecyclerView is constant. The height (or width) of the item won't change. Every item added or removed will be the same. If you dont set this it will check if the size of the item has changed and thats expensive.

#### RecyclweView SnapHelper
SnapHelper is a helper class that helps in snapping any child view of the RecyclerView.
For example set a child to snap at the start, end or center of the screen.


### Dialog and DialogFragment
#### Dialog
A dialog is a small window that prompts the user to make a decision or enter additional information. A dialog does not fill the screen and is normally used for modal events that require users to take an action before they can proceed.

#### DialogFragment
A DialogFragment is a special fragment subclass that is designed for creating and hosting dialogs. It allows the FragmentManager to manage the state of the dialog and automatically restore the dialog when a configuration change occurs.

DialogFragment is basically a Fragment that can be used as a dialog.

Using DialogFragment over Dialog due to the following reasons:

- DialogFragment is automatically re-created after configuration changes and save & restore flow
- DialogFragment inherits full Fragment’s lifecycle
- No more IllegalStateExceptions and leaked window crashes. This was pretty common when the activity was destroyed with the Alert Dialog still there.

### Toast and Snackbar
A toast provides simple feedback about an operation in a small popup.
Snackbars inform users of a process that an app has performed or will perform.

### Distinct Apps Interanction

Sending the User to Another App using Intents.

Getting a Result from an Activity. Registering a callback `registerForActivityResult`

### Run an Android app in multiple processes
You can specify `android:process=":remote"` in your manifest to have an activity/service run in a seperate process.

The "remote" is just the name of the remote process, and you can call it whatever you want. If you want several activities/services to run in the same process, just give it the same name.

### IInterface descriptioon language (IDL)
An interface description language or interface definition language (DL), is a generic term for a language that lets a program or object written in one language communicate with another program written in an unknown language. 
IDLs describe an interface in a language-independent way, enabling communication between software components that do not share one language, for example, between those written in C++ and those written in Java.

#### Aidl
The Android Interface Definition Language (AIDL) is similar to other [IDLs](https://en.wikipedia.org/wiki/Interface_description_language) you might have worked with. It allows you to define the programming interface that both the client and service agree upon in order to communicate with each other using interprocess communication (IPC). On Android, one process cannot normally access the memory of another process. So to talk, they need to decompose their objects into primitives that the operating system can understand, and marshall the objects across that boundary for you. The code to do that marshalling is tedious to write, so Android handles it for you with AIDL.

1. Create the .aidl file
You must construct the `.aidl` file using the Java programming language. Each `.aidl` file must define a single interface and requires only the interface declaration and method signatures.

2. Implement the interface
 When you build your application, the Android SDK tools generate a `.java` interface file named after your `.aidl` file. The generated interface includes a subclass named `Stub` that is an abstract implementation of its parent interface (for example, `YourInterface.Stub`) and declares all the methods from the `.aidl` file.
 
3. Expose de interface to clients
Once you've implemented the interface for your service, you need to expose it to clients so they can bind to it. To expose the interface for your service, extend `[Service](https://developer.android.com/reference/android/app/Service)` and implement `[onBind()](https://developer.android.com/reference/android/app/Service#onBind(android.content.Intent))` to return an instance of your class that implements the generated `Stub` (as discussed in the previous section). Here's an example service that exposes the `IRemoteService` example interface to clients.

### Background processing

#### Common background tasks

The following list shows common tasks that an app manages while it runs in the background:

- Your appregisters a broadcast receiverin the manifest file.
- Your app schedules a repeating alarm using Alarm Manager.
- Your app schedules a background task, either as a worker using Work Manager or a job using Job Scheduler.

#### Categories of background tasks

Background tasks fall into one of the following main categories:

##### Immediate tasks
if we need to run it while the user interacts with the app


We recommend [Kotlin coroutines](https://developer.android.com/kotlin/coroutines) for tasks that should end when the user leaves a certain scope or finishes an interaction. Many [Android KTX](https://developer.android.com/kotlin/ktx) libraries contain ready-to-use coroutine scopes for common app components like [`ViewModel`](https://developer.android.com/topic/libraries/architecture/coroutines#viewmodelscope) and common application [lifecycles](https://developer.android.com/topic/libraries/architecture/coroutines#lifecyclescope).

For Java programming language users, see [Threading on Android](https://developer.android.com/guide/background/threading) for recommended options.

For tasks that should be executed immediately and need continued processing, even if the user puts the application in background or the device restarts, we recommend using [`WorkManager`](https://developer.android.com/topic/libraries/architecture/workmanager) and its support for [long-running tasks](https://developer.android.com/topic/libraries/architecture/workmanager/advanced/long-running).

In specific cases, such as with media playback or active navigation, you might want to use [foreground Services](https://developer.android.com/guide/components/services#Foreground) directly.

##### Exact tasks

A task that needs to be executed at an exact point in time can use [`AlarmManager`](https://developer.android.com/reference/android/app/AlarmManager).

To learn more about `AlarmManager`, see [Schedule alarms](https://developer.android.com/training/scheduling/alarms).

##### Expedited tasks

A task that needs to run as soon as possible can start an _expedited job_ using [expedited work](https://developer.android.com/topic/libraries/architecture/workmanager/how-to/define-work#expedited).

##### Deferred tasks

Every task that is not directly connected to a user interaction and can run at any time in the future can be deferred. The recommended solution for deferred tasks is [`WorkManager`](https://developer.android.com/topic/libraries/architecture/workmanager).

`WorkManager` makes it easy to schedule deferrable, asynchronous tasks that are expected to run even if the app exits or the device restarts. See the documentation for [`WorkManager`](https://developer.android.com/topic/libraries/architecture/workmanager) to learn how to schedule these types of tasks.

### Processes
By default, all components of the same application run in the same process and most applications should not change this. However, if you find that you need to control which process a certain component belongs to, you can do so in the manifest file.

### Threads

When an application is launched, the system creates a thread of execution for the application, called "main." This thread is very important because it is in charge of dispatching events to the appropriate user interface widgets, including drawing events. It is also almost always the thread in which your application interacts with components from the Android UI toolkit (components from the `[android.widget](https://developer.android.com/reference/android/widget/package-summary)` and `[android.view](https://developer.android.com/reference/android/view/package-summary)` packages). As such, the main thread is also sometimes called the UI thread. However, under special circumstances, an app's main thread might not be its UI thread; for more information, see [Thread annotations](https://developer.android.com/studio/write/annotations#thread-annotations).

The system does _not_ create a separate thread for each instance of a component. All components that run in the same process are instantiated in the UI thread, and system calls to each component are dispatched from that thread. Consequently, methods that respond to system callbacks (such as `[onKeyDown()](https://developer.android.com/reference/android/view/View#onKeyDown(int, android.view.KeyEvent))` to report user actions or a lifecycle callback method) always run in the UI thread of the process.

For instance, when the user touches a button on the screen, your app's UI thread dispatches the touch event to the widget, which in turn sets its pressed state and posts an invalidate request to the event queue. The UI thread dequeues the request and notifies the widget that it should redraw itself.

When your app performs intensive work in response to user interaction, this single thread model can yield poor performance unless you implement your application properly. Specifically, if everything is happening in the UI thread, performing long operations such as network access or database queries will block the whole UI. When the thread is blocked, no events can be dispatched, including drawing events. From the user's perspective, the application appears to hang.

#### Background thread
Any thread that is not the Main or Ui which we execute to get some result would be the background thread.

##### How does AsyncTask helps to achieve background execution?
AsyncTask creates a worker Theard and execute the task in that Thread.

##### How to update the UI thrugh AsyncTask?
`doInBackground` will do the operation in the worker thread
`onPostExecute` will post the result on the Main thread and we can update the UI there

##### Asynchronous behaviour
If we have

AsyncTask A
AsyncTask B
AsyncTask C

And we do
A.execute()
B.execute()
C.execute()

AsyncTask by default creates a single Worker thread for the whole application.
So A, B, C will be executed serially.

##### How to run A, B, C in parallel?
In order to make it run in parallel we need to use `executeOnExecutor` and pass the Thread pool executor.

##### What happens if A, B, C were running and the Activity was back pressed?
They will execute on its own without any interference of the Activity and when they finish, `onPostExecute` will be called.

If we update the UI and the activity is destroyed,then the view may be destroyed as well, this will cause and Exception as we are referencing a memory of a view that does not exists.

One solution would be to:
Create a new AsyncTask that extendes from AsyncTask, take a callback object and keep it in a weak reference because the callback may be implemented in the Activity and we don't want to hold a reference to the Activity, and then we check if the callback is not null in `onPostExecute`.

Other solutions would be Loaders or ViewModel.


#### Explain `Looper`, `Handler` and `HandlerThread`

`Looper`, `Handler`, and `HandlerThread` are the Android’s way of solving the problems of asynchronous programming.

**_What is the problem with java thread?_**

Java threads are one-time use only and die after executing its run method.

**_Can we improve upon it?_**

The Thread is a double edged sword. We can speed up the execution by distributing the tasks among threads of execution, but can also slow it down when threads are in excess. Thread creation in itself is an overhead. So, the best option is to have an optimum number of threads and reuse them for tasks execution.

**_What is the Android’s way of doing it?_**

The above model is implemented in the Android via `Looper`, `Handler`, and `HandlerThread`. The System can be visualized to be a vehicle as in the article’s cover.

1.  `MessageQueue` is a queue that has tasks called messages which should be processed.
2.  `Handler` enqueues task in the `MessageQueue` using `Looper` and also executes them when the task comes out of the `MessageQueue`.
3.  `Looper` is a worker that keeps a thread alive, loops through `MessageQueue` and sends messages to the corresponding `handler` to process.
4.  Finally `Thread` gets terminated by calling Looper’s `quit()` method.

 _One thread can have only one unique Looper and can have many unique Handlers associated with it._
 
 Creating an own thread and providing `Lopper` and `MessageQueue` is not the right way to deal with the problem. So, Android has provided `HandlerThread`(_subclass of_ `Thread`) to streamline the process. Internally it does the same things that we have done but in a robust way. So, always use `HandlerThread`.
 
 
 ```kotlin
  
class Worker() : Thread() {  

    private val tasks = ConcurrentLinkedQueue<Runnable>()  
    private val alive = AtomicBoolean(true)  
    
    init {  
        start()  
    }  
    
    override fun run() {  
        while (alive.get()) {  
           tasks.poll()?.run()  
        } 
        //  "worker terminated"  
    }  

    fun execute(task: Runnable): Worker{  
        tasks.add(task)  
        return this  
    }  

    fun quit(){  
        alive.set(false)  
    }
}  

class WorkerHandler: HandlerThread("Handler"){  

    private var handler: Handler  

    init {  
        start()  
        handler = Handler(looper)  
    }  
    
    fun execute(task: Runnable): WorkerHandler{  
        handler.post(task)  
        return this  
    }  
}
```

### Memory
**Heap** **memory** is a part of **memory** allocated to JVM, which is shared by all executing threads in the application. It is the part of JVM in which all class instances and are allocated. It is created on the Start-up process of JVM. It does not need to be contiguous, and its size can be static or dynamic.

#### Memory heap vs Memory stack

##### Stack
 - uses LIFO(Last in , first out) algorithm
 - can only remove the last item you added and it used for local variables sinde they come and go as the exceution enters and exits functions and it does not work well whose lifecyle does not depende on individual exits functions, its very limited
 - used for static memory allocation
 - momery allocation happens when the program is compiled

##### Heap

Heap is the area in the memory which is used to store objects, memory is not managed automatically, there is no size limit, and objects in the heap are slower to access that in the stack because of its algorith it uses

 - heap is used for dynamic memory allocation, memory allocation begins at runtime

This is managed by the JVM and uses the Garbage Collection( is an algorithm runing in java in the background)

Android’s memory heap is a generational one, meaning that there are different buckets of allocations that it tracks, based on the expected life and size of an object being allocated. For example, recently allocated objects belong in the _Young generation_. When an object stays active long enough, it can be promoted to an older generation, followed by a permanent generation.

Each heap generation has its own dedicated upper limit on the amount of memory that objects there can occupy. Any time a generation starts to fill up, the system executes a garbage collection event in an attempt to free up memory. The duration of the garbage collection depends on which generation of objects it's collecting and how many active objects are in each generation.

#### Memory leak
Java stores the object in heap storage and is cleared by the garbage collection. Memory leak take place when object remain in memory even when it is not required and can not be garbage collected. This result from a component with longer life holding the reference of a component with smaller life.

A memory leak is when the avelaible space in the heap can not be used to store an object that i desire, meaning it still being referenced by a component that its lifecyle is more that the one not being referenced, this is called **hard reference**.

#### Garbage colector GC
Searches the heap for nodes that are null, meanin that are not referenced anywhere else in the heap

Minor/ short Gc runs in parallerl in another thread and wont freeze the ui, runs from 2-5 ms

Large GC runs in the main thread and will rearenge the node, called **Compaction**

Will rearage memory to make space for a new object and will freeze the ui, runs from 50-100 ms

 - atomic variables like AtomicBoolean can't be seen while changing, and ensure that not more that one thread is changin the variable at the same time
 - static means it will be shared among all object
 - syncronized block tells the compiler tha only onw thread is allowed to enver this block at the same time and it works on the memory, appliygin visibility like volatile to all variables in th block
 - volatile will make it visible in the main memory, meaning it wont be cached and every time we need it we will need to find it in the main memory, avoiding a  cach version that was old maybe

#### onTrimMemory()

Android can reclaim memory from your app in several ways or kill your app entirely if necessary to free up memory for critical tasks. To further help balance the system memory and avoid the system's need to kill your app process, you can implement the `[ComponentCallbacks2](https://developer.android.com/reference/android/content/ComponentCallbacks2)` interface in your `[Activity](https://developer.android.com/reference/android/app/Activity)` classes. The provided `[onTrimMemory()](https://developer.android.com/reference/android/content/ComponentCallbacks2#onTrimMemory(int))` callback method allows your app to listen for memory related events when your app is in either the foreground or the background, and then release objects in response to app lifecycle or system events that indicate the system needs to reclaim memory.

### Database 
**Normalization** is the process of organizing data in a **database**. This includes creating tables and establishing relationships between those tables according to rules designed both to protect the data and to make the **database** more flexible by eliminating redundancy and inconsistent dependency.

#### ORM
**ORM** stands for object-relational mapping, where objects are used to connect the programming language on to the **database** systems

Room is an ORM, a wrapper around SQLite, it maps entitys to  the databse.

Room has:
 - database, managa sql like operatios, making queires
 - entity, mapping over the table
 - dao, provides queries over the entity / table / database

#### Save state in an Activity
 - For simple data, the activity can use the onSaveInstanceState() method and restore its data from the bundle in onCreate(), but this approach is only suitable for small amounts of data that can be serialized then deserialized, not for potentially large amounts of data like a list of users or bitmaps.
 - For large data use viewModel

### Scoped Storage

#### Internal Storage

When you install some application on your phone, then the Android system will provide you with some kind of private internal storage where the application can store its private data. This data can't be accessed by any other application. When you uninstall the application, then all the data related to that application will be deleted.

#### External Storage

Most of the Android devices have very less internal storage. So, we use some kind of external storage unit to store our data. These storage unit are accessed by everyone i.e. it can be accessed by all the applications in your device. Also, you can access the storage just by connecting the mobile device to some PC.

#### Shared Preferences

If you have a small amount of data to store and you don't want to use the internal storage, then you can use the shared preferences. Shared Preferences are used to store the data in the form of key-value i.e. you will be having one key and based on that key, the corresponding data or value will be stored.

#### Database

Databases are organised collection of data that are stored for future reference. You can store any kind of data in your Database by using some Database Management System. All you need to do is just create the database and do all the operation i.e. insertion, deletion, searching, etc with the help of one query. You will pass the query and the database will return the desired output from the database. SQLite database is one such example of a database in Android.

---

The idea of the Scoped Storage is to compartmentalize the storage into specified collections to limit the access to broad storage. There are certain principles on which the Scoped Storage is based on:

-   **Better Attribution:** Better attribution means the system knows which file is generated by which application. The benefit of doing this is, you will have better management of files of a particular application. Also, when you uninstall an application from the device then all the contents related to the app will also be removed unless the user explicitly wants to keep it.
-   **App data protection:** As we know that the internal storage of the app is private and can't be accessed by other applications. But the external storage is accessed by applications with storage permission. With the help of Scoped Storage, the data in the external storage can not be easily accessed by other applications.

###   What is commit() and apply() in SharedPreferences?
   - commit() returns a boolean value of success or failure immediately by writing data synchronously.
   - apply() is asynchronous and it won't return any boolean response. If you have an apply() outstanding and you are performing commit(), then the commit() will be blocked until the apply() is not completed.

### Bitmap
#### What is the difference between a regular `Bitmap` and a nine-patch image?
In general, a Nine-patch image allows resizing that can be used as background or other image size requirements for the target device. The Nine-patch refers to the way you can resize the image: 4 corners that are unscaled, 4 edges that are scaled in 1 axis, and the middle one that can be scaled into both axes.

_Nine-Patch File_, A `PNG` file with stretchable regions to allow image resizing based on content (.9.png), creates a `NinePatchDrawable`.

#### Bitmap vs drawable
A Bitmap is a pixel holder, and canvas is iused to dra somehitng on bitmap pixels.

A Bitmap is a representation of a bitmap image (something like java.awt.Image). A Drawable is an abstraction of "something that can be drawn". It could be a Bitmap (wrapped up as a `BitmapDrawable`), but it could also be a solid color, a collection of other Drawable objects, or any number of other structures.

Most of the Android UI framework likes to work with Drawable objects, not Bitmap objects. A View can accept any Drawable as a background. An ImageView can display a foreground Drawable. Images stored as resources are loaded as Drawable objects.

#### Bitmap pool
Basically means that instead of recycling and old bitmap and allocating new memory to show another bitmap we can reuse the old bitmap memory space, it has to be the same exact size in orther to do so.

We do this using `inBitmap` with `BitmapFactoryy.Options()`
If set, decode methods that take the Options object will attempt to reuse this bitmap when loading content. If the decode operation cannot use this bitmap, the decode method will throw an [IllegalArgumentException](https://developer.android.com/reference/java/lang/IllegalArgumentException)

Also exists object pools with the same idea .

#### PNG compression

PNG compression is lossless, we can compress and decompress it without losing quality.

1. Filtering, using the diference from the pxiel to the near pixels we can express it as the difference
2. Deflate, we look from the same value in the png to compress all similar values using the same way/ diffrence

### Spans
Spans are powerful concepts that allow styling text at character or paragraph levels by providing access to components like TextPaint and Canvas.

Article with a lot of info 
https://medium.com/androiddevelopers/underspanding-spans-1b91008b97e4

### Strings
#### String

A `String` is immutable (ie, the text can't change). It also doesn't have any spans associated with it. (Spans are ranges over the text that include styling information like color, highlighting, italics, links, etc.) So you can use a `String` when your text doesn't need to be changed and doesn't need any styling.

#### StringBuilder

A `StringBuilder` has mutable text, so you can modify it without creating a new object. However, it doesn't have any span information. It is just plain text. So use a `StringBuilder` when you need to change the text, but you don't care about styling it.

#### SpannedString

A `SpannedString` has immutable text (like a `String`) and immutable span information. It is a concrete implementation of the requirements defined by the [`Spanned`](https://developer.android.com/reference/android/text/Spanned.html) interface. Use a `SpannedString` when your text has style but you don't need to change either the text or the style after it is created.

_Note:_ There is no such thing as a `SpannedStringBuilder` because if the text changed then the span information would also very likely have to change.

#### SpannableString

A `SpannableString` has immutable text, but its span information is mutable. It is a concrete implementation of the requirements defined by the [`Spannable`](https://developer.android.com/reference/android/text/Spannable.html) interface. Use a `SpannableString` when your text doesn't need to be changed but the styling does.

#### SpannableStringBuilder

A `SpannableStringBuilder` has both mutable text and span information. It is a concrete implementation of the requirements defined by the [`Spannable`](https://developer.android.com/reference/android/text/Spannable.html) and [`Editable`](https://developer.android.com/reference/android/text/Editable.html) interfaces (among others). Use a `SpannableStringBuilder` when you will need to update the text and its style.

#### CharSequence

A `CharSequence` is an interface and not a concrete class. That means it just defines a list of rules to follow for any class that implements it. And all of the classes mentioned above implement it. So you can use a `CharSequence` when you want to generalize the type of object that you have for maximum flexibility. You can always downcast it to a `String` or `SpannableStringBuilder` or whatever later if you need to.

### Pixel density

**Density Independent Pixels** —an abstract unit that is based on the physical density of the screen. These units are relative to a _160_ dpi screen, so one dp is one pixel on a _160_ dpi screen. The ratio of dp-to-pixel will change with the screen density, but not necessarily in direct proportion. "Density independence" refers to the uniform display of UI elements on screens with different densities.

**Scale Independent Pixels** —This is same as dp, but by default, android resizes it based on the font size of the user’s phone.

stands for scalable pixels. Generally _sp_ is used for texts on the UI, and _sp_ preserves the font settings. For example, if a user selected a larger font than _30 sp_ it will auto-scale to appear large according to a user preference.

### Doze and App Stanby
#### Doze
If a user leaves a device unplugged and stationary for a period of time, with the screen off, the device enters Doze mode. In Doze mode, the system attempts to conserve battery by restricting apps' access to network and CPU-intensive services. It also prevents apps from accessing the network and defers their jobs, syncs, and standard alarms.

Periodically, the system exits Doze for a brief time to let apps complete their deferred activities. During this _maintenance window_, the system runs all pending syncs, jobs, and alarms, and lets apps access the network.

#### Stanby
App Standby allows the system to determine that an app is idle when the user is not actively using it. The system makes this determination when the user does not touch the app for a certain period of time and none of the following conditions applies:

-   The user explicitly launches the app.
-   The app has a process currently in the foreground (either as an activity or foreground service, or in use by another activity or foreground service).
-   The app generates a notification that users see on the lock screen or in the notification tray.
-   The app is an active device admin app (for example, a [device policy controller](https://developer.android.com/work/dpc/build-dpc)). Although they generally run in the background, device admin apps never enter App Standby because they must remain available to receive policy from a server at any time.

When the user plugs the device into a power supply, the system releases apps from the standby state, allowing them to freely access the network and to execute any pending jobs and syncs. If the device is idle for long periods of time, the system allows idle apps network access around once a day.

### Permissions 
1.  Normal Permissions . If there is a very little or no risk of the user privacy then the permission comes under the Normal Permission category. Like internet permission
2.  Signature Permissions. 
The android system grants these permissions at the installation time but there is one condition. The app that is asking for some permission must be signed with the same signature as that of the app that defines the required permission. Following are some of the Signature permissions,like write / read voicemail
3.  Dangerous Permissions. 
Dangerous permissions include that permission that involve user data in some or the other way.
To use Dangerous permissions, you have to explicitly ask for permission before using that by showing some alert dialog or any other dialog. If the user denies the permission then your application can’t use that particular permission.

#### Special permissions
These are those permissions that are neither Normal permissions nor Dangerous permissions. Most of the applications should not use these permissions because they are very sensitive and you need user authorization before using these permissions. To use this permission, you must declare it in the **_AndroidManifest.xml_** file and then send an intent to request for user authorization. Some of the Special permissions are:

1.  WRITE_SETTINGS
2.  SYSTEM_ALERT_WINDOW

These are the three main protection levels of permissions, apart from this there is one more protection level called the Special Permission. Let’s have a look at them, one by one.

### NKD
Android Ndk - Native Development Kit is a toolset that lets you implement parts of your app in native code, using 
languages such as C and C++. It helps in making the applications run fast and also in reusable code in other platforms. 

we create a c file and compile it, it will compile into native code file

then we use a JNI (java native interface) is the bridge to interact with the native code file(.so)

example: reading every pixel in a bitmap,
instead of loading the bitmap in java we load it in C passing the path and then do the operationm there for the whole bitmap, then return the path

### RenderScript 
RenderScript is a framework for running computationally intensive tasks at high performance on Android.

RenderScript mainly uses for the data-parallel computation, however, the serial computationally intensive workloads can benefit as well.

The RenderScript runtime will parallelize work across all processors available on a device such as multi-core CPUs and GPUs allowing you to focus on expressing algorithms rather than scheduling work or load balancing.

RenderScript is especially useful for applications performing image processing, computational photography, or computer vision.

To begin with RenderScript, there are two main concepts you should understand:

-   High-performance compute kernels are written in a C99-derived language.
-   A Java API is used for managing the lifetime of RenderScript resources and controlling kernel execution.

#### How NDK and RenderScript differ

As we know both NDK and RenderScript share the common goal of improving the performance of applications. However, each has its own advantages and drawbacks.

**Advantages of NDK over RenderScript:**

-   C++ code can be shared between Android and IOS, whereas RenderScript code can be used only in Android.
-   Easy integration with other C++ libraries.
-   No API limitations, while Android provides only a few API for RenderScript.
-   Debugging is easier.

### Dalvik vs ART
Our computer only understands the Machine level language but we write code in some High-level language. Same is with Android also, in Android, your Java classes will be converted into DEX bytecode and this DEX bytecode format is translated to Machine code with the help of ART or Dalvik runtimes.

#### What is Dalvik?

Dalvik is a Just In Time (JIT) compiler. By the term JIT, we mean to say that whenever you run your app in your mobile device then that part of your code that is needed for execution of your app will only be compiled at that moment and rest of the code will be compiled in the future when needed. The JIT or Just In Time compiles only a part of your code and it has a smaller memory footprint and due to this, it uses very less physical space on your device.

#### What is ART?

ART or Android Runtime is an Android runtime that uses Ahead Of Time(AOT). By using AOT, what is does is it converts or compiles the whole High-level language code into Machine level code and at the time of installation of the app and not dynamically as the application runs(like in case of Dalvik). By compiling the whole code during installation results in no lag that we see when we run our app on our device. By doing so, the compilation becomes very faster. Following are some of the words about ART from the Android Developers website:

 _ART is a new Android runtime being introduced experimentally in the 4.4 release KitKat. This is a preview of work in progress in KitKat. It is available for obtaining early developer and partner feedback._
 
 ### Why Android use Virtual Machine?

Android makes use of a virtual machine as its runtime environment in order to run the APK files that constitute an Android application. Below are the advantages:

· The application code is isolated from the core OS. So even if any code contains some malicious code won’t directly affect the system files. It makes the Android OS more stable and reliable.

· It provides cross compatibility or platform independency. It meaning even if an app is compiled on platform such as a PC, it can still be executed on the mobile platform using the virtual machine.

### Android Jetpack

Android Jetpack is a collection of Android software components which helps us in building great Android apps.

These software components help in:

-   Following the best practices and writing the boilerplate code.
-   Making complex things very simple.

Earlier there were many challenges which are as follows:

-   Managing activity lifecycles.
-   Surviving configuration changes.
-   Preventing memory leaks.

All these major problems have been solved by the Android Jetpack's software components.

So, the solution for all the problems is Andriod Jetpack.

Another most important thing about the Jetpack is that it gets updated more frequently than the Android platform so that we always get the latest version.

Jetpack comprises the [androidx.*](https://developer.android.com/jetpack/androidx) package libraries, unbundled from the platform APIs. This means that it offers backward compatibility.

Software compoennts

The foundation components provide the following:
Android KTX, app compat

-   Backward compatibility
-   Testing
-   Kotlin language support.
---

The architecture components help us in building:

-   Robust Apps
-   Testable Apps
-   Maintainable Apps

All the Android Architecture Components are as follows:

-   [Data Binding](https://developer.android.com/topic/libraries/data-binding/): It helps in declaratively binding UI elements to in our layout to data sources of our app.
-   [Lifecycles](https://developer.android.com/topic/libraries/architecture/lifecycle): It manages activity and fragment lifecycles of our app, survives configuration changes, avoids memory leaks and easily loads data into our UI.
-   [LiveData](https://developer.android.com/topic/libraries/architecture/livedata): It notifies views of any database changes. Use [LiveData](https://developer.android.com/topic/libraries/architecture/livedata) to build data objects that notify views when the underlying database changes.
-   [Navigation](https://developer.android.com/topic/libraries/architecture/navigation/): It handles everything needed for in-app navigation in Android application.
-   [Paging](https://developer.android.com/topic/libraries/architecture/paging/): It helps in gradually loading information on demand from our data source.
-   [Room](https://blog.mindorks.com/android-room-persistence-library-in-kotlin): It is a SQLite object mapping library. Use it to Avoid boilerplate code and easily convert SQLite table data to Java objects. Room provides compile time checks of SQLite statements and can return RxJava, Flowable and LiveData observables.
-   [ViewModel](https://developer.android.com/topic/libraries/architecture/viewmodel): It manages UI-related data in a lifecycle-conscious way. It stores UI-related data that isn't destroyed on app rotations.
-   [WorkManager](https://developer.android.com/topic/libraries/architecture/workmanager/): It manages every background jobs in Android with the circumstances we choose.
---

The behavior components help in the integration with standard Android services like
permissions, media player, preferences

-   Notifications
-   Permissions
-   Sharing
-   Assistant

The UI components provide widgets and helpers to make your app not only easy, but delightful to use.
Like fragments, layour, pallete

### LiveData
LiveData is an observable data holder class. Unlike a regular observable, LiveData is lifecycle-aware, meaning it respects the lifecycle of other app components, such as activities, fragments, or services. This awareness ensures LiveData only updates app component observers that are in an active lifecycle state.

#### LiveData vs Observable Field
ObservableField is not Lifecycle aware but LiveData is. That means LiveData will only update app component observers that are in an active lifecycle state and not which are inactive.
    
#### postValue vs setValue
So, the duty of the `postValue` method is to post or add a task to the main thread of the application whenever there is a change in the value. And the value will be updated whenever the main thread will be executed. So, basically, it is requesting the main thread to set the new updated value and then notify the observers.

While the `setValue` method is used to set the changed value from the main thread and if there are some live observers to it, then the updated value will also be sent to those observers as well. **This `setValue` method must be called from the main thread.**

So, here are some of the points that you must think before using `setValue` and `postValue`:

-   If you are working on the main thread, then both `setValue` and `postValue` will work in the same manner i.e. they will update the value and notify the observers.
-   If working in some background thread, then you can't use `setValue`. You have to use `postValue` here with some observer. But the interesting thing about `postValue` is that the value will be change immediately but the notification that is to be sent to observers will be scheduled to execute on the main thread via the event loop with the handler.

### What is Work Manager?

Work Manager is a library part of Android Jetpack which makes it easy to schedule deferrable, asynchronous tasks that are expected to run even if the app exits or device restarts i.e. even your app restarts due to any issue Work Manager makes sure the scheduled task executes again.

### How ViewModel work internally
 The viewmodels are stored inside the activity (or `` `FragmentManager` `` in case of fragments).
 
 1.  Creation of `` `ViewModelProvider` ``
2.  Getting the instance of `` `Viewmodel` `` from `` `ViewModelProvider` ``

viewModelProvider requires Viewmodel stor and factory(to pass args)

`` `ViewModelStoreOwner` `` is a simple interface with a single method named `` `getViewModelStore()` ``

In the constructor, we are simply getting the `` `ViewModelStore` `` from `` `ViewModelStoreOwner` `` and passing it to the other constructor where they are just assigned to the respective class members.

When we invoke `` `get()` `` method on our `` `ViewModelProvider` ``, it gets the **canonical name** of the view model class and creates a key by appending the **canonical name** to a **_DEFAULT_KEY_**.

After creating the key from the model class, it checks the `` `ViewModelStore` `` (which is provided by our activity) whether a `` `viewmodel` `` instance for the given key is already present or not. If the `` `viewmodel` `` is already present, it simply returns the `` `viewmodel` `` instance present in `` `ViewModelStore` `` and if it’s not present, the `` `ViewModelProvider` `` uses the `` `Factory` `` instance to create a new `` `viewmodel` `` object and also stores it in `` `ViewModelStore` ``.

> _Note:_ _`` `ViewModels` ``_ _are not retained directly. Instead,_ _`` `ViewModelStore` ``_ _is retained on configuration changes which internally maintains a map of_ _`` `viewmodels` ``._

### Parcelable vs Serializable
#### Serializable

[Serializable](https://docs.oracle.com/javase/7/docs/api/java/io/Serializable.html) is a standard Java interface. It is not a part of the Android SDK. It’s simplicity is it’s beauty. Just by implementing this interface your POJO will be ready to jump from one Activity to another. In the following code snippet you can see how simple it is to use this interface.

Reflection is used during the process and lots of additional objects are created along the way.

#### Parcelable

[Parcelable](https://developer.android.com/reference/android/os/Parcelable.html) is another interface. Despite it’s rival (Serializable in case you forgot), it is a part of the Android SDK. Now, Parcelable was specifically designed in such a way that there is no reflection when using it.

### Reflection
**Java** **Reflection** **is** a process of examining or modifying the run time behavior of a class at run time

### IPC
Inter-process communication (IPC) is a mechanism that allows processes to communicate with each other and synchronize their actions. The communication between these processes can be seen as a method of co-operation between them. Processes can communicate with each other through both:
1.  Shared Memory
2.  Message passing

### AAPT2
AAPT2 (Android Asset Packaging Tool) is a build tool that Android Studio and Android Gradle Plugin use to compile and package your app’s [resources](https://developer.android.com/guide/topics/resources/providing-resources). AAPT2 parses, indexes, and compiles the resources into a binary format that is optimized for the Android platform.

Android Gradle Plugin 3.0.0 and higher enable AAPT2 by default, and you typically won't need to invoke `aapt2` yourself. However, if you prefer to use your terminal and your own build system over Android Studio, you can use AAPT2 from the command line. You can also debug build errors related to AAPT2 from the command line. To do so, you can find AAPT2 as a standalone tool in [Android SDK Build Tools](https://developer.android.com/studio/releases/build-tools) 26.0.2 and higher.

### Annotations
Annotations allow you to provide hints to code inspections tools like Lint, to help detect these more subtle code problems. They are added as metadata tags that you attach to variables, parameters, and return values to inspect method return values, passed parameters, local variables, and fields. When used with code inspections tools, annotations can help you detect problems, such as null pointer exceptions and resource type conflicts.

### Support Libraries
When developing apps that support multiple API versions, you may want a standard way to provide newer features on earlier versions of Android or gracefully fall back to equivalent functionality. Rather than building code to handle earlier versions of the platform, you can leverage these libraries to provide that compatibility layer. In addition, the Support Libraries provide additional convenience classes and features not available in the standard Framework API for easier development and support across more devices.

### viewTreeObserver
A view tree observer is used to register listeners that can be notified of global changes in the view tree. Such global events include, but are not limited to, layout of the whole tree, beginning of the drawing pass, touch mode change.... A ViewTreeObserver should never be instantiated by applications as it is provided by the views hierarchy

### Data Binding
The Data Binding Library is a support library that allows you to bind UI components in your layouts to data sources in your app using a declarative format, rather than programmatically.

Data Binding allows you to effortlessly communicate across views and data sources.

Data binding is the process of integrating views in an XML layout with data objects. The Data Binding Library is responsible for generating the classes required for this procedure.

### What is RxJava?

RxJava is used for reactive programming. In reactive programming, the consumer reacts to the data as it comes in. Reactive programming allows for event changes to propagate to registered observers.

### Exception

#### What are exceptions in Android ?

**Exceptions** are events that occur during the execution of programs that disrupt the normal flow. They are of two types : **Checked** and **Unchecked**.

-   Checked Exception : Exception that must be either caught or declared in the method in which it is thrown. For example,

```java
String transform(String input) throws IOException;
```

-   UnChecked Exception : The Exceptions whose handling is NOT verified during Compile time. For example,

```java
if (i == 3) {
    throw NullPointerException("Its a NPE")
}
```


### How Glide or image libraries works
**When we provide the URL to the Glide, it does the following:**

1.  It checks if the image with that URL key is available in the memory cache or not.
2.  If present in the memory cache, it just shows the bitmap by taking it from the memory cache.
3.  If not present in the memory cache, it checks in the disk cache.
4.  If present in the disk cache, it loads the bitmap from the disk, also puts it in the memory cache and load the bitmap into the view.
5.  If not present in the disk cache, it downloads the image from the network, puts it in the disk cache, also puts it in the memory cache and load the bitmap into the view.

This way it makes loading fast as showing directly from the memory cache is always faster.

### DI (Dependency Injection)
Dependency Injection in build upon the concept of Inversion of Control which says that a class should get its dependencies from outside. In simple words, no class should instantiate another class but should get the instances from a configuration class.

Consider, that when we have to create a lot of objects which are dependent on many other objects in our project, it becomes tough when the project becomes bigger.
With the code base increasing, we might need some good external support to manage it all. That is one of the use-cases for that we use a **dependency framework**

#### Module
Sometimes a type cannot be constructor-injected. This can happen for multiple reasons. For example, you cannot constructor-inject an interface. You also cannot constructor-inject a type that you do not own, such as a class from an external library. In these cases, you can provide Hilt with binding information by using _Hilt modules_.

A Hilt module is a class that is annotated with `@Module`. Like a [Dagger module](https://developer.android.com/training/dependency-injection/dagger-android#dagger-modules), it informs Hilt how to provide instances of certain types. Unlike Dagger modules, you must annotate Hilt modules with `@InstallIn` to tell Hilt which Android class each module will be used or installed in.

#### Component
Dagger can create a graph of the dependencies in your project that it can use to find out where it should get those dependencies when they are needed. To make Dagger do this, you need to create an interface and annotate it with `@Component`. Dagger creates a container as you would have done with manual dependency injection.

Inside the `@Component` interface, you can define functions that return instances of the classes you need (i.e. `UserRepository`). `@Component` tells Dagger to generate a container with all the dependencies required to satisfy the types it exposes. This is called a _Dagger component_; it contains a graph that consists of the objects that Dagger knows how to provide and their respective dependencies.

Acts as a bridge from the module and class to be injected, there is no need for this with Hilt.

For field injection we need to add a inject method in the component passing the Activity / Fragment, then create the component and inject it in the onCreate method for example, this will populate all the variable with inject.

For consturctor  injection there is no need for the second part. We just acces the component and then from there the variable or what we are injecting.

### Testing
#### Espresso
Use Espresso to write concise, beautiful, and reliable Android UI tests.

```kotlin
@Test  
fun greeterSaysHello() { 
    onView(withId(R.id.name_field)).perform(typeText("Steve")) 
    onView(withId(R.id.greet_button)).perform(click()) 
    onView(withText("HelloSteve!")).check(matches(isDisplayed()))  
}
```

#### Roboelectric
[Robolectric](http://robolectric.org/) is a framework that brings fast and reliable unit tests to Android. Tests run inside the JVM on your workstation in seconds. With Robolectric you can write tests like this:

```java
@RunWith(RobolectricTestRunner.class)
public class MyActivityTest {

  @Test
  public void clickingButton_shouldChangeMessage() {
    MyActivity activity = Robolectric.setupActivity(MyActivity.class);

    activity.button.performClick();

    assertThat(activity.message.getText()).isEqualTo("Robolectric Rocks!");
  }
}
```


##### Roboelectric vs Android test framework
You would use **Robolectric** only in cases you need to mock or fake the **Android framework**, e.g. if you need a context. When using the **Android Test Framework** you would have to run **Instrumented tests** for that which is ultra slow.

#### UIAutomator
UI Automator is a UI testing framework suitable for cross-app functional UI testing across system and installed apps. The UI Automator APIs let you interact with visible elements on a device, regardless of which [`Activity`](https://developer.android.com/reference/android/app/Activity) is in focus, so it allows you to perform operations such as opening the Settings menu or the app launcher in a test device. Your test can look up a UI component by using convenient descriptors such as the text displayed in that component or its content description.

#### Unit test
A _local_ test runs directly on your own workstation, rather than an Android device or emulator. As such, it uses your local Java Virtual Machine (JVM), rather than an Android device to run tests.

Test of single uints of our app. ( example testing the functions of a class) 
Made to run very often.

#### Instrumental test(ui test)
Instrumented tests run on Android devices, whether physical or emulated. As such, they can take advantage of the Android framework APIs. Instrumented tests therefore provide more fidelity than local tests, though they run much more slowly.

#### Integration tests
Test how to components of our app work together( ex fragment and viewmodel)

#### Integrated test
Are test that relied on android components(ex context, activity) and must be run on the emulator

#### JUnit
**JUnit** is a [unit testing](https://en.wikipedia.org/wiki/Unit_testing "Unit testing") [framework](https://en.wikipedia.org/wiki/Software_framework "Software framework") for the [Java programming language](https://en.wikipedia.org/wiki/Java_(programming_language) "Java (programming language)").

#### Mockito
Mocks a class that has all the functions of that class but without implementation

Example:
 1. We can mock NavController
 2. Perfrom a click on a button that navigates to a fragment
 3. Check navController.navigate(//fragment id) was called

### What makes a good test?
- Scope, how much of our code is covered by our single test
- Speed
- Fidelity: how close is the test case to a real scenario

Avoid flaky test: test that sometimes succeeds and sometimes fails

### Android Debug Nridge(adb)
Android Debug Bridge (adb) is a versatile command-line tool that lets you communicate with a device.

Use for ex: installing apps, debuggin them, copying files from the debvice, set ports

### Lint and Strictmode
Lint is a code scanning tool provided by the Android Studio to identify, suggest and correct the wrong or the risky code present in the project.

 - Lint is for compiling
 - Strictmode is the same but for run time, meaning when the app is running its only for debug

### Firebase remote config
Firebase Remote Config, we can bring some updates in the App like some text change, color change in the Android App, without publishing any update of the app on the Play Store.

### Gradle
So, simply putting, it is an automation tool that generates the application build. Gradle is the official build tool for Android.

### Module
_A **module** is a collection of source files and build settings that allow you to divide your project into discrete units of functionality. Your project can have one or many modules and one module may use another module as a dependency. Each module can be independently built, tested, and debugged._

### Dex
In Java, if we compile our code then that code is converted into a **_.class_** file by the compiler because our machine understands that **_.class_** file. The same is the process for the Android Application. In Android, the compiler converts our source code into **DEX**(Dalvik Executable) file.

The build process of a typical Android App can be summarized as below:

1.  The compilers convert the source code into DEX (Dalvik Executable) files, which include the bytecode that runs on Android devices.
2.  After having the DEX files, the APK Packager combines the DEX files and compiled resources into a single APK.
3.  After that, the APK Packager signs the APK.
4.  Before generating the final APK, various methods are followed to optimize the code so as to avoid the unused code.

In Android, the compilers convert your source code into DEX files. This DEX file contains the compiled code used to run the app. But there is a limitation with the DEX file. The DEX file limits the total number of methods that can be referenced within a single DEX file to 64K i.e. 65,536 methods. So, you can't use more than 64K methods in a particular DEX file. These 64K methods include Android framework methods, library methods, and methods in our code also. This limit of 64K is referred to as the "**64K reference limit

Multidex create mutiple dex files so we can have more that 64k methods.

It causes erros in api lower that 21
If your secondary dex file is larger that the primary dex file, it might encoutner aplication not respodong error (ANR)

### Proguard
ProGuard is a free java tool in Android, which helps us to do the following,

-   Shrink(Minify) the code: Remove unused code in the project.
-   Obfuscate the code: Rename the names of class, fields, etc.
-   Optimize the code: Do things like inlining the functions.

In short, ProGuard makes the following impact on our project,

-   It reduces the size of the application.
-   It removes the unused classes and methods that contribute to the 64K method counts limit of an Android application.
-   It makes the application difficult to reverse engineer by obfuscating the code.

### LinearLayout

[LinearLayout](https://www.geeksforgeeks.org/linearlayout-and-its-important-attributes-with-examples-in-android/) is a type of view group which is responsible for holding views in it either Horizontally or vertically. It is a type of Layout where one can arrange groups either Horizontally or Vertically.

### RelativeLayout

[RelativeLayout](https://www.geeksforgeeks.org/android-relativelayout-in-kotlin/) is a layout in which we can arrange views/widgets according to the position of other view/widgets. It is independent of horizontal and vertical view and we can arrange it according to one’s satisfaction.

### Pass data between activities
Add data in intent with `intent.putExtra(key,value)`, also in value we can use bundle.

### Android ABIs
Different Android devices use different CPUs, which in turn support different instruction sets. Each combination of CPU and instruction set has its own Application Binary Interface (ABI).

### Log
 - log v : send verbose message
 - log d: debug
 - log i : info
 - log w: warn
 - log e : error

### Bundle
`Bundle` is: a collection of key-value pairs.

### Loader

The Loader API lets you load data from a [content provider](https://developer.android.com/guide/topics/providers/content-providers) or other data source for display in an `[FragmentActivity](https://developer.android.com/reference/androidx/fragment/app/FragmentActivity)` or `[Fragment](https://developer.android.com/reference/androidx/fragment/app/Fragment)`. If you don't understand why you need the Loader API to perform this seemingly trivial operation, then first consider some of the problems you might encounter without loaders:

-   If you fetch the data directly in the activity or fragment, your users will suffer from lack of responsiveness due to performing potentially slow queries from the UI thread.
-   If you fetch the data from another thread, perhaps with `[AsyncTask](https://developer.android.com/reference/android/os/AsyncTask)`, then you're responsible for managing both the thread and the UI thread through various activity or fragment lifecycle events, such as `[onDestroy()](https://developer.android.com/reference/android/app/Activity#onDestroy())` and configurations changes.

Loaders solve these problems and includes other benefits. For example:

-   Loaders run on separate threads to prevent janky or unresponsive UI.
-   Loaders simplify thread management by providing callback methods when events occur.
-   Loaders persist and cache results across configuration changes to prevent duplicate queries.
-   Loaders can implement an observer to monitor for changes in the underlying data source. For example, `[CursorLoader](https://developer.android.com/reference/androidx/loader/content/CursorLoader)` automatically registers a `[ContentObserver](https://developer.android.com/reference/android/database/ContentObserver)` to trigger a reload when data changes.


### System tracing

Recording device activity over a short period of time is known as _system tracing_. System tracing produces a trace file that can be used to generate a system report. This report helps you identify how best to improve your app or game's performance.

The Android platform provides several different options for capturing traces:

-   Android Studio CPU profiler
-   System tracing utility
-   Perfetto command-line tool (Android 10 and higher)
-   Systrace command-line tool

We can use Perfetto Ui to analize the files that the emularo/ phon creates

### REST - Representation state  transfer o transferencia de presentacion de estado
REST is an architectural style used to create APIs taht allow us to connect our servers with clients using HTTP protocol with URIs smart enough to meet the client needs.

REST es STATELESS, As per the REST (REpresentational **“State”** Transfer) architecture, the server does not store any state about the client session on the server-side. This restriction is called **Statelessness**.

Each request from the client to the server must contain all of the necessary information to understand the request. The server cannot take advantage of any stored context on the server.

### RESTfull
It's the implementation of REST, doing this we create an API, which is a software intermediary that allows two applications to talk to each other.