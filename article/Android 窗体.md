# Android 窗体

## Activity

### 通过 ActivityThread 中的 performLaunchActivity 方法 创建了对应的 Activity，先调用了 Activity 的 attach 方法，再通过 mInstrumentation 调用了 Activity 的 onCreate 方法

### Windows

- Windows 是有个抽象类，它的唯一实现类是 PhoneWindows 类
- WindowsManager

	- 如何创建

		- 在 Activity 的 attach 方法中创建完 PhoneWindows 赋给 Windows，调用 Windows 的 setWindowManager 方法创建了WindowsManager，这个方法中是通过 WindowManagerImpl 的 createLocalWindowManager() 方法创建的

		  在 Windows 的 setWindowManager 方法中，首先获取系统启动注册的 WindowManager，系统是通过 WindowManagerImpl(ctx) 创建的，我们拿到 WindowManager，通过 ((WindowManagerImpl)wm).createLocalWindowManager(windows) 方法创建了一个新的 WindowsManagerImpl，与 Windows 相关联

	- WindowsManager 和 DecorView 是在什么时候进行绑定的

		- ActivityThread 中启动 Activity 时候先调用了 handleLaunchActivity 方法，在这个方法中调用完 performLaunchActivity 方法，又调用了 handleResumeActivity 方法，进行绑定的过程是在 handleResumeActivity 方法中，通过WindowsManager 的 addView 方法把 DecorView 绑定

	- WindowsManager 是一个接口，具体的实现类是 WindowManagerImpl，它是通过 WindowManagerGlobal 代理实现
	- WindowManagerGlobal

		- 其内部通过 ViewRootImpl 来管理 View
		- ViewRootImpl

### IBinder : mToken

## PhoneWindows 

### 如何创建的

- 在 Activity 中的 attach 方法中创建了 PhoneWindows

### DecorView

- 作用

	- 添加标题栏和内容，PhoneWindows 是它的载体

- 如何创建的

	- 它继承了 FrameLayout，通过 PhoneWindows 中的 generateDecor 方法创建的

- 不同版本问题

	- 从 Android 7.0 开始 DecorView 是一个单独类，之前的版本 DecorView 是PhoneWindows 的内部类

### mContentParent

- 通过 generateLayout(DecorView decor) 方法把返回值赋给 mContentParent，mContentParent 是我们的内容区域，在这个方法中，会获取用户设置的主题等属性，因此 requesetFeature 方法必须在 setContentView 方法之前调用