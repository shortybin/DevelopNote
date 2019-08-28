1. Fragment 的 onAttach(Activity) 方法在 API 23 之后被弃用，改为 onAttach(Context) ，所以针对不同的 SDK 版本使用不同的方法。例子：
```

   @TargetApi(23)
   @Override  
   public void onAttach(Context context) {  
       super.onAttach(context);  
       // 执行操作 
   }  
  
   /* 
    * Deprecated on API 23 
    * Use onAttachToContext instead 
    */  
   @SuppressWarnings("deprecation")  
   @Override  
   public void onAttach(Activity activity) {  
       super.onAttach(activity);  
       if (Build.VERSION.SDK_INT < Build.VERSION_CODES.M) {  
            // 执行操作 
       }  
   }  
```
Fragment 中，如果要获取 Activity 对象，不建议调用 getActivity() ，而是在 onAttach() 中将 Context 对象强转为 Activity 对象。

2. AtomicLong 和 Long 的区别是？

   AtomicLong 是线程安全的，Long 是线程不安全的。

3. GestureDetector 的作用是什么？
    
    GestureDetector 是一个手势监听识别的类，其有两个接口 OnGestureListener，OnDoubleTapListener 和一个静态内部类 SimpleOnGestureListener。这个内部类实现了提供的两个接口。具体实例如下：
```
GestureDetector detector = new GestureDetector(this, new GestureDetector.SimpleOnGestureListener() {
            //需要处理什么手势，重写相应的回调方法
            @Override
            public boolean onDoubleTap(MotionEvent e) {
                //双击的回调
                return super.onDoubleTap(e);
            }
        });

view.setOnTouchListener(new View.OnTouchListener() {
            @Override
            public boolean onTouch(View v, MotionEvent event) {
                detector.onTouchEvent(event);
                return false;
            }
        });
```
4. Android 中在 WebView 中访问微信的支付页面，打不开的问题

```
mWebview.setWebViewClient(new WebViewClient() {
            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                // 如下方案可在非微信内部WebView的H5页面中调出微信支付
                if (url.startsWith("weixin://wap/pay?")) {
                    Intent intent = new Intent();
                    intent.setAction(Intent.ACTION_VIEW);
                    intent.setData(Uri.parse(url));
                    startActivity(intent);
                    return true;
                }
                view.loadUrl(url);
                return true;
            }

            @Override
            public void onPageFinished(WebView view, String url) {
                // 这个方法有可能会多次执行
                super.onPageFinished(view, url);
            }
        });
```
5. Activity 的生命周期 A 启动 B 的生命周期流程

    A:onCreate->A:onStart->A:onResume->A:onPause->B:onCreate->B:onStart->B:onResume->A:onStop

6. ToolBar 左侧有一个默认的左边距，不去掉导致与设计页面不符
    
```
通过给 ToolBar 设置 app:contentInsetStart="0dp" 属性可以去除默认的左边距
```
7. ARouter 设置了 withFlags 必须需要在 navigation 中设置 Activity，不然会报 Calling startActivity() from outside of an Activity context requires the FLAG_ACTIVITY_NEW_TASK flag. 如果不添加 withFlags，ARouter 会自动给不是 Activity 的添加 FLAG_ACTIVITY_NEW_TASK flag。

```
ARouter.getInstance().build(RouterConfig.APPLICATION_ACTIVITY).withFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP).navigation(Actvity.this);
```
8. View 的 scrollTo() 和 scrollBy() 方法移动方向

```
当水平方向为正值，向左侧移动，为负值向右侧移动。
当垂直方向为正值，向上移动，为负值向下移动。
```
9.Webview 的 clearHistory() 方法不起作用的解决

```
clearHistory() 作用是调用方法时，清空当前页面之前的所有记录

方法1:postDelayed 延时调用
webView.postDelayed(new Runnable() {
    @Override
    public void run() {
        webView.clearHistory();
    }
}, 1000);

方法2:在 onPageFinished 方法中去调用 clearHistory 方法
```
10. Android 7.0 以上 AES 加密报错 java.security.NoSuchAlgorithmException: class configured for SecureRandom (provider: Crypto) cannot be found.

[InsecureSHA1PRNGKeyDerivator 工具类的下载地址](https://github.com/shrotybin/DevelopNote/blob/master/utils/InsecureSHA1PRNGKeyDerivator.java)
```
解决方法
private static byte[] getRawKey(byte[] seed) throws Exception {
        if (Build.VERSION.SDK_INT >= 24) {//对 9.0 以上的进行处理
            byte[] rawKey = InsecureSHA1PRNGKeyDerivator.deriveInsecureKey(seed, 32);
            return rawKey;
        } else {
            KeyGenerator kgen = KeyGenerator.getInstance(AES);
            //for android
            SecureRandom sr = null;
            // 在4.2以上版本中，SecureRandom获取方式发生了改变
            if (android.os.Build.VERSION.SDK_INT >= 17) {
                sr = SecureRandom.getInstance(SHA1PRNG, "Crypto");
            } else {
                sr = SecureRandom.getInstance(SHA1PRNG);
            }
            // for Java
            // secureRandom = SecureRandom.getInstance(SHA1PRNG);
            sr.setSeed(seed);
            kgen.init(128, sr); //256 bits or 128 bits,192bits
            //AES中128位密钥版本有10个加密循环，192比特密钥版本有12个加密循环，256比特密钥版本则有14个加密循环。
            SecretKey skey = kgen.generateKey();
            byte[] raw = skey.getEncoded();
            return raw;
        }
    }
```
11. 在 Android P 上弹窗提示 Detected problems with API compatibility(visit g.co/dev/appcompat for more info)

```
Android P 后谷歌限制了开发者调用非官方公开 API 方法或接口，如果通过反射调用了非官方的 API 就会提示这个弹窗，建议查找代码去掉相应的反射。
```
12. Android 9.0 网络请求报 java.net.UnknownServiceException: CLEARTEXT communication ** not permitted by network security policy 

```
在Android P 系统的设备上，如果应用使用的是非加密的明文流量的 http 网络请求，则会导致该应用无法进行网络请求，https 则不会受影响，同样地，如果应用嵌套了 webview，webview 也只能使用 https 请求。

解决办法：1.将请求替换未 https
2. 在 res 下新增一个 xml 目录，然后创建一个名为：network_security_config.xml 文件（名字自定） ，内容如下，大概意思就是允许开启 http 请求

<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
 <base-config cleartextTrafficPermitted="true" />
</network-security-config>

然后在APP的AndroidManifest.xml文件下的application标签增加以下属性


<application
...
 android:networkSecurityConfig="@xml/network_security_config"
...
/>
```
13. Android 9.0 上报 ClassNotFoundException: Didn't find class "org.apache.http.conn.scheme.SchemeRegistry

[官方给出的解释](https://developer.android.google.cn/about/versions/pie/android-9.0-changes-28)
```
在 Android 6.0 中，我们取消了对 Apache HTTP 客户端的支持。 从 Android 9 开始，默认情况下该内容库已从 bootclasspath 中移除且不可用于应用。

解决办法:在 AndroidManifest.xml 的 application 节点下添加以下内容：

<uses-library android:name="org.apache.http.legacy" android:required="false"/>
```
14. Android 使用三方库一般都需要在 Application 中做一些初始化，使用 ContentProvider，可以将初始化放到库中自定义的 ContentProvider 中让主 APP 使用，因为 ContentProvider 的初始化是在 Application 之中进行的。
15. Android 8.0 某些手机会报 java.lang.IllegalStateException: Only fullscreen opaque activities can request orientation

```
方案 1:去除 android:screenOrientation="portrait"，或者不调用设置方向的代码
方案 2:设置 <item name="android:windowIsTranslucent">false</item>
<item name="android:windowIsFloating">false</item>
```
16. Android 原生 webview 加载出现页面部分内容不显示，日志报了 This request has been blocked; the content must be served over HTTPS.

```
这个是加载的地址是https的，一些资源文件使用的是http方法的，从安卓4.4之后对webview安全机制有了加强，webview里面加载https url的时候，如果里面需要加载http的资源或者重定向的时候，webview会block页面加载。需要设置MixedContentMode。

如下设置：
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
            // 5.0以上允许加载http和https混合的页面(5.0以下默认允许，5.0+默认禁止)
            webSettings.setMixedContentMode(WebSettings.MIXED_CONTENT_ALWAYS_ALLOW);
}

```
17. 当一个类的方法被 protected 修饰，只有在同一个包下才能被调用，要想在别的包下调用可以用匿名内部类的方式

```
Gson 的 TypeToken 构造函数是 protected。
TypeToken<List<String>> list = new TypeToken<List<String>>() {};
```
18. 数字保留两位小数的方法

```
DecimalFormat decimalFormat = new DecimalFormat("0.00");
String format = decimalFormat.format(mPrice);
```
19. 报错信息:Bitmap: Error, cannot access an invalid/free'd bitmap here!

```
debug 后也发现是在 nativeColorSpaceCopy 这里出问题，因此不要手动 recycle()
去掉手动调用 bitmap 的 recycle() 方法即可。
```
20. Java 集合的总结

```
jdk 1.6中如下，别的版本有所不同
HashMap 的默认大小为16，阀值为0.75，扩容大小为（当前大小+当前大小*0.75），线程不安全，数据结构为数组加单向链表组成的哈希表结构，键值对允许为null。
HashTable 的默认大小为11，阀值为0.75，扩容大小为（当前大小*2+1），线程安全，数据结构为数组加单向链表组成的哈希表结构，键值对不允许为null。
ArrayList 的默认大小为10，扩容大小为（当前大小*1.5+1），线程不安全，数据结构为动态数组，可以添加null。
LinkedList 的默认大小为10，因为是双向链表所以无需扩容，线程不安全，可以添加null。
HashSet 内部使用了 HashMap 的 Key 来存储数据，他的数据不能重复。
```
21. Java 内部类的问题

```
1.内部类中不能包含静态方法，必须为静态内部类包含静态方法。
2.静态内部类不能直接直接访问外部类的非静态属性
```
22. Android 某些机型拍照出来的照片默认旋转了90度，如果我们要加载图片应该先获取图片旋转了多少度，然后再旋转回去显示
```
获取图片旋转的角度
public static int readPictureDegree(String path) {
        int degree = 0;
        try {
            ExifInterface exifInterface = new ExifInterface(path);
            int orientation = exifInterface.getAttributeInt(
                    ExifInterface.TAG_ORIENTATION,
                    ExifInterface.ORIENTATION_NORMAL);
            switch (orientation) {
                case ExifInterface.ORIENTATION_ROTATE_90:
                    degree = 90;
                    break;
                case ExifInterface.ORIENTATION_ROTATE_180:
                    degree = 180;
                    break;
                case ExifInterface.ORIENTATION_ROTATE_270:
                    degree = 270;
                    break;
            }
        } catch (IOException e) {
            e.printStackTrace();
            return degree;
        }
        return degree;
    }
```

















   

