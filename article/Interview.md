# 面试经历

## 1. 屏幕适配都是怎们去做的
 1. 尽量使用相对布局(RelativeLayout)，禁用绝对布局(AbsoluteLayout)。LinearLayout使用"wrap_content"和"match_parent"已经可以构建出不错的布局。但是LinearLayout无法准确地控制子视图之间的位置关系，只能简单的一个挨着一个地排列，所以对于适配屏幕应该根据情况适当选择。
 2. 根据屏幕的配置来加载相应的UI布局。
   * 尺寸限定符：根据不同的屏幕尺寸加载不同的布局(这种方式只适合Android 3.2版本之前)。
   * 最小宽度限定符：根据设定的不同宽度，不同的屏幕宽度加载不同的布局(Android 3.2版本之后引入的，推荐使用)。
   * 屏幕方向限定分：根据屏幕的方向加载不同的布局。
 3. 组件的宽高使用dp，字体的大小使用sp
 4. 使用"wrap_content"、"match_parent"和"weight“来控制视图组件的宽度和高度，尽量少使用dp直接控制宽高
 5. 对于图片在不同屏幕密度上显示相同的像素效果，使用.9图
 6. 使用百分比适配
 7. 不同分辨率使用多套图片资源，考虑APK太大，可以只用xhdpi

## 2. equals 和 == 的区别
  == 用来比较基本类型，equals 一般用来比较引用类型的。使用==比较引用类型，比较的是对象的地址。自定义对象的 euqals 方法内部使用的 == 来比较的,继承自Object。如果自定义的对象要比较，可以重写 equals 方法，重写 equals 方法注意必须先要重写 hashCode 方法（这一点给忘记了。。。）。
## 3. MVC和MVP优缺点
### MVC:
  * View：视图界面，对应于布局文件
  * Model：数据的封装和保存，业务逻辑和实体模型
  * Controller：业务逻辑，对应于Activity、Fragment等

### MVC的优点:
  * 比较容易理解，对于一些小的项目维护和迭代比较方便

### MVC的缺点:
  * Activity 即充当了 View 又充当了 Controller，分工不明确
  * 对于一些复杂的功能，Activity内的代码太多（多达几千行），难以维护和迭代
  * View和Model之间相互可知，存在耦合
  * 不利于单元测试

### MVP:
  * View：对应于Activity，负责View的绘制以及与用户交互
  * Model：依然是业务逻辑和实体模型
  * Presenter：负责完成View于Model间的交互

### MVP优点:
  * 解耦，三个层级之间互相不知道各自的内容
  * 各个层级之间结构清晰，易于维护
  * 业务逻辑单独出来，易于单元测试

### MVP缺点:
  * 接口比较多
  * 在一些小的项目上使用反而没有MVC开发快速

## 4. 重写和重载的不同
### 重写:
  * 父类与子类之间的多态性，对父类的函数进行重新定义。如果在子类中定义某方法与其父类有相同的名称和参数，我们说该方法被重写 (Overriding)。在Java中，子类可继承父类中的方法，而不需要重新编写相同的方法。但有时子类并不想原封不动地继承父类的方法，而是想作一定的修改，这就需要采用方法的重写。方法重写又称方法覆盖
  * 若子类中的方法与父类中的某一方法具有相同的方法名、返回类型和参数表，则新方法将覆盖原有的方法。如需父类中原有的方法，可使用super关键字，该关键字引用了当前类的父类
  * 子类函数的访问修饰权限不能少于父类的

### 重写的规则
  * 参数列表必须完全与被重写的方法相同，否则不能称其为重写而是重载
  * 返回的类型必须一直与被重写的方法的返回类型相同，否则不能称其为重写而是重载
  * 访问修饰符的限制一定要大于被重写方法的访问修饰符（public>protected>default>private）
  * 重写方法一定不能抛出新的检查异常或者比被重写方法申明更加宽泛的检查型异常。例如：父类的一个方法申明了一个检查异常IOException，在重写这个方法是就不能抛出Exception,只能抛出IOException的子类异常，可以抛出非检查异常

### 重载
  * 方法重载是让类以统一的方式处理不同类型数据的一种手段。多个同名函数同时存在，具有不同的参数个数/类型。重载Overloading是一个类中多态性的一种表现。
  * Java的方法重载，就是在类中可以创建多个方法，它们具有相同的名字，但具有不同的参数和不同的定义。调用方法时通过传递给它们的不同参数个数和参数类型来决定具体使用哪个方法, 这就是多态性。
  * 重载的时候，方法名要一样，但是参数类型和个数不一样，返回值类型可以相同也可以不相同。无法以返回型别作为重载函数的区分标准。

### 重载的规则
  * 必须具有不同的参数列表；
  * 可以有不同的返回类型，只要参数列表不同就可以了；
  * 可以有不同的访问修饰符；
  * 可以抛出不同的异常；

### 重写和重载的不同之处
##### 重写多态性起作用，对调用被重载过的方法可以大大减少代码的输入量，同一个方法名只要往里面传递不同的参数就可以拥有不同的功能或返回值。用好重写和重载可以设计一个结构清晰而简洁的类，可以说重写和重载在编写代码过程中的作用非同一般.
## 5. 栈和队列的区别
### 队列：是限定只能在表的一端进行插入和在另一端进行删除操作的线性表。
### 栈：是限定只能在表的一端进行插入和删除操作的线性表。

栈和队列的区别如下：

  * 规则不同
     1. 队列：先进先出
     2. 栈：先进后出
  * 对插入和删除操作的限定不同
     1. 队列：只能在表的一端进行插入，并在表的另一端进行删除；
     2. 栈：只能在表的一端插入和删除。
  * 遍历数据速度不同
     1. 队列：基于地址指针进行遍历，而且可以从头部或者尾部进行遍历，但不能同时遍历，无需开辟空间，因为在遍历的过程中不影响数据结构，所以遍历速度要快；
     2. 栈：只能从顶部取数据，也就是说最先进入栈底的，需要遍历整个栈才能取出来，而且在遍历数据的同时需要为数据开辟临时空间，保持数据在遍历前的一致性。

## 6. List、Map和Set的不同
这一块的内容比较多，推荐一个链接大家直接看吧！！！<http://blog.csdn.net/vstar283551454/article/details/8682655>。 这一块的内容比较重要的，基本面试都会问到，而且会结合到数据结构的内容，大家平时多看看相关的内容，最好可以深入到源码。
## 7. 创建线程有几种方法
Java中创建线程共三种方法：

  * 继承Thread类创建线程类
    1. 定义Thread类的子类，并重写该类的run方法，该run方法的方法体就代表了线程要完成的任务。因此把run()方法称为执行体。
    2. 创建Thread子类的实例，即创建了线程对象。
    3. 调用线程对象的start()方法来启动该线程。
  * 通过Runnable接口创建线程类
    1. 定义 Runnable 接口的实现类，并重写该接口的run()方法，该run()方法的方法体同样是该线程的线程执行体。
    2. 创建 Runnable 实现类的实例，并依此实例作为Thread的target来创建Thread对象，该Thread对象才是真正的线程对象。
    3. 调用线程对象的start()方法来启动该线程。
  * 通过Callable和Future创建线程（这种方法使用的较少）
    1. 创建Callable接口的实现类，并实现call()方法，该call()方法将作为线程执行体，并且有返回值。
    2. 创建Callable实现类的实例，使用FutureTask类来包装Callable对象，该FutureTask对象封装了该Callable对象的call()方法的返回值。
    3. 使用FutureTask对象作为Thread对象的target创建并启动新线程。
    4. 调用FutureTask对象的get()方法来获得子线程执行结束后的返回值

各个创建线程的优缺点：

Runnable、Callable优势是：
线程类只是实现了Runnable接口或Callable接口，还可以继承其他类。在这种方式下，多个线程可以共享同一个target对象，所以非常适合多个相同线程来处理同一份资源的情况，从而可以将CPU、代码和数据分开，形成清晰的模型，较好地体现了面向对象的思想。

缺点是：
编程稍微复杂，如果要访问当前线程，则必须使用Thread.currentThread()方法。

继承Thread类的方式的优势是：
编写简单，如果需要访问当前线程，则无需使用Thread.currentThread()方法，直接使用this即可获得当前线程。

缺点是：
线程类已经继承了Thread类，所以不能再继承其他父类。
## 8. 线程间通信有几种方法
  * 通过发送广播
  * Activity的runOnUiThread(Runnable r)方法（内部借助Handler）
  * View对象的post(Runnable r)或postDelay(Runnable r)方法（内部借助Handler）
  * Handler实现线程间的通信
  * 使用AsyncTask（内部封装了Handler）
  * 使用EventBus、RxJava等框架

## 9. 进程通信有几种方法
  * Android的四大组件都可以进行进程通信
  * 使用AIDL进行进程通信
  * 通过隐式Intent
  * 文件共享，对同一个文件先后进行读写，但要注意同步
  * 使用Socket，服务中定义 ServerSocket 来监听端口，客户端使用 Socket 来请求端口，连通后就可以进行通信

## 10. Service保活有什么方法
  * 提高服务的优先级
  * 使用双服务守护进程
  * 在屏幕上保留一个像素点
  这些方法都没发达到完全保活，不同的系统上可能没发保证不被杀死。而且Service一直在运行时比较消耗电量的，Google也不建议开发者让Service一直运行。

## 11. Activity和Fragment通信有那几种方法
  * Fragment和Fragment通信，一个Fragment可以直接调另一个Fragment中的方法
  * Activity和Fragment通信可以使用接口回调的方式
  * 两个Fragment通信可以使用广播
  * Fragment可以直接调用Activity里public的方法

## 12. View的绘制流程
  View的绘制流程大致分为三部：Measure -> Layout -> Draw。具体每个过程大家可以详细的了解下具体的过程。这一块问了之后一般都会问到自定义View。
## 13. 事件分发流程
  1. 事件从Activity.dispatchTouchEvent()开始传递，只要没有被停止或拦截，从最上层的View(ViewGroup)开始一直往下(子View)传递。子View可以通过onTouchEvent()对事件进行处理。
  2. 事件由父View(ViewGroup)传递给子View，ViewGroup可以通过onInterceptTouchEvent()对事件做拦截，停止其往下传递。
  3. 如果事件从上往下传递过程中一直没有被停止，且最底层子View没有消费事件，事件会反向往上传递，这时父View(ViewGroup)可以进行消费，如果还是没有被消费的话，最后会到Activity的onTouchEvent()函数。
  4. 如果View没有对ACTION_DOWN进行消费，之后的其他事件不会传递过来。
  5. OnTouchListener优先于onTouchEvent()对事件进行消费。

  这个问题基本是每次面试都会问到的。

## 14. Handler机制
  从Handler中获取一个消息对象，把数据封装到消息对象中，通过Handler的send…方法把消息push到MessageQueue队列中。 Looper对象会轮询MessageQueue队列，把消息对象取出。 通过dispatchMessage分发给Handler，再回调用Handler实现的handleMessage方法处理消息。

  这个是一个大概的描述，在详细的流程大家可以去搜索下，网上相关的介绍非常多，而且很多都是带有图片分析，更容易理解。这个在面试中也是经常问到的。

## 15. TCP和UDP不同
  1. TCP面向连接（如打电话要先拨号建立连接）;UDP是无连接的，即发送数据之前不需要建立连接
  2. TCP提供可靠的服务。也就是说，通过TCP连接传送的数据，无差错，不丢失，不重复，且按序到达;UDP尽最大努力交付，即不保证可靠交付
  3. TCP面向字节流，实际上是TCP把数据看成一连串无结构的字节流;UDP是面向报文的,UDP没有拥塞控制，因此网络出现拥塞不会使源主机的发送速率降低（对实时应用很有用，如IP电话，实时视频会议等）
  4. 每一条TCP连接只能是点到点的;UDP支持一对一，一对多，多对一和多对多的交互通信
  5. TCP首部开销20字节;UDP的首部开销小，只有8个字节
  6. TCP的逻辑通信信道是全双工的可靠信道，UDP则是不可靠信道

## 16. 内存泄露有哪些
  1. 集合类导致泄露，集合内添加了元素，一直未删除
  2. 使用单例造成泄漏，传入了Activity造成
  3. 匿名内部类/非静态内部类和异步线程
  4. Handler 造成的内存泄漏，Handler 发送的 Message 尚未被处理，则该 Message 及发送它的 Handler 对象将被线程 MessageQueue 一直持有。
  5. 资源未关闭造成的内存泄漏
  6. Bitmap 没调用 recycle()方法，Bitmap 对象在不使用时,我们应该先调用 recycle() 释放内存。

  对于内存泄漏可以集成 LeakCanary 分析出什么地方存在内存泄漏，及时修改。

## 17. 性能优化如何做
  1. 布局的层级不要太深，如过嵌套过多，渲染比较慢
  2. 使用 Leakcanary 工具定位分析内存泄漏
  3. 图片优化，尽量使用比较小的图片，图片要缓存和复用
  4. 存储的集合对象及时清理
  5. 使用IntentService代替Service

这个相关的方法特别多，我就不一一列举了，大家有需要的去搜索吧！！！ 这个问题每次面试都问到
## 18. 图片缓存的原理
  Android 图片的缓存有三级缓存：内存、文件、网络。

  图片加载这一块现在我们用的都是第三方的框架，很少使用自己写的缓存，要想知道具体的原理，大家可能需要研究下图片加载框架的内部实现原理了，大概知道下三级缓存是怎么做的，心里有个数，面试的时候能大概说出来就行。查看框架的源码还是十分重要，公司都比较看重员工的自学能力。
## 19. 线程池内部是如何实现的
  1. 判断线程池里的核心线程是否都在执行任务，如果不是（核心线程空闲或者还有核心线程没有被创建）则创建一个新的工作线程来执行任务。如果核心线程都在执行任务，则进入下个流程。
  2. 线程池判断工作队列是否已满，如果工作队列没有满，则将新提交的任务存储在这个工作队列里。如果工作队列满了，则进入下个流程。
  3. 判断线程池里的线程是否都处于工作状态，如果没有，则创建一个新的工作线程来执行任务。如果已经满了，则交给饱和策略来处理这个任务。
  
## 20. Mediaplay的生命周期

### Mediaplay的生命周期顺序是：Idle -> Initialized -> Prepared -> Preparing -> Started -> Paused -> Stop -> PlaybackCompleted -> End -> Error

* Idle：当使用new()方法创建一个MediaPlayer对象或者调用了其reset()方法时，该MediaPlayer对象处于idle状态。这两种方法的一个重要差别就是：如果在这个状态下调用了getDuration()等方法（相当于调用时机不正确），通过reset()方法进入idle状态的话会触发OnErrorListener.onError()，并且MediaPlayer会进入Error状态；如果是新创建的MediaPlayer对象，则并不会触发onError(),也不会进入Error状态。

* End: 通过release()方法可以进入End状态，只要MediaPlayer对象不再被使用，就应当尽快将其通过release()方法释放掉，以释放相关的软硬件组件资源，这其中有些资源是只有一份的（相当于临界资源）。如果MediaPlayer对象进入了End状态，则不会在进入任何其他状态了。

* Initialized:这个状态比较简单，MediaPlayer调用setDataSource()方法就进入Initialized状态，表示此时要播放的文件已经设置好了。

* Prepared:初始化完成之后还需要通过调用prepare()或prepareAsync()方法，这两个方法一个是同步的一个是异步的，只有进入Prepared状态，才表明MediaPlayer到目前为止都没有错误，可以进行文件播放。

* Preparing:这个状态比较好理解，主要是和prepareAsync()配合，如果异步准备完成，会触发OnPreparedListener.onPrepared()，进而进入Prepared状态。

* Started:显然，MediaPlayer一旦准备好，就可以调用start()方法，这样MediaPlayer就处于Started状态，这表明MediaPlayer正在播放文件过程中。可以使用isPlaying()测试MediaPlayer是否处于了Started状态。如果播放完毕，而又设置了循环播放，则MediaPlayer仍然会处于Started状态，类似的，如果在该状态下MediaPlayer调用了seekTo()或者start()方法均可以让MediaPlayer停留在Started状态。

*  Paused:Started状态下MediaPlayer调用pause()方法可以暂停MediaPlayer，从而进入Paused状态，MediaPlayer暂停后再次调用start()则可以继续MediaPlayer的播放，转到Started状态，暂停状态时可以调用seekTo()方法，这是不会改变状态的。

*  Stop:Started或者Paused状态下均可调用stop()停止MediaPlayer，而处于Stop状态的MediaPlayer要想重新播放，需要通过prepareAsync()和prepare()回到先前的Prepared状态重新开始才可以。
  
*  PlaybackCompleted:文件正常播放完毕，而又没有设置循环播放的话就进入该状态，并会触发OnCompletionListener的onCompletion()方法。此时可以调用start()方法重新从头播放文件，也可以stop()停止MediaPlayer，或者也可以seekTo()来重新定位播放位置。
  
*  Error:如果由于某种原因MediaPlayer出现了错误，会触发OnErrorListener.onError()事件，此时MediaPlayer即进入Error状态，及时捕捉并妥善处理这些错误是很重要的，可以帮助我们及时释放相关的软硬件资源，也可以改善用户体验。通过setOnErrorListener(android.media.MediaPlayer.OnErrorListener)可以设置该监听器。如果MediaPlayer进入了Error状态，可以通过调用reset()来恢复，使得MediaPlayer重新返回到Idle状态。

## 21. 图片加载框架volley、glider的实现

## 22. 插件化和热修复的原理
## 23. UI层数据和服务器数据不一样，如何解析数据
## 24. 涟漪的自定义View实现
## 25. 数据库使用sqllite还是provider，哪一个会更好一些
## 26. App自动更新如何实现，断点续传的原理
## 27. Https和Http的区别，Http如何保障访问安全


## 总结
  这个文章里面总结面试中遇到的问题，答案基本上都来自网络，如有侵犯可联系我，我会加上链接地址。另外有些没有给出答案，大家可以自己总结。如果答案存在问题或者有需要补充的大家可以提 Issues

  参考：
  <http://blog.csdn.net/vstar283551454/article/details/8682655>

******
