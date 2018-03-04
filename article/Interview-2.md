# 最近面试中遇到的题目：
## 1. 屏幕旋转时 Activity 的生命周期变化(测试Android版本为7.1.1,版本号为25)

   configChanges 是默认的情况下，由竖屏切换为横屏时生命周期时：
   
   onPause()——>onStop()——>onDestroy()——>onCreate()——>onStart()——>onResume()
   
   再有横屏切换为竖屏时，生命周期为：
   
   onPause()——>onStop()——>onDestroy()——>onCreate()——>onStart()——>onResume()
   
   configChanges 设置为 "orientation|keyboardHidden" 时，由竖屏切换为横屏时生命周期为：
   
   onPause()——>onStop()——>onDestroy()——>onCreate()——>onStart()——>onResume()
   
   再由横屏切换为竖屏时，生命周期为：
   
   onPause()——>onStop()——>onDestroy()——>onCreate()——>onStart()——>onResume()
   
   configChanges 设置为 "orientation|keyboardHidden|screenSize" 时，由竖屏切换为横屏时生命周期为：
   
   onConfigurationChanged()
   
   再由横屏切换为竖屏时，生命周期为：
   
   onConfigurationChanged(）
  
## 2. Fragment 切换的方式有几种，它的生命周期变化
 参考链接：<http://blog.csdn.net/hjiangshujing/article/details/52367734>
  
## 3. Android 中动画的原理
 参考链接：<https://www.cnblogs.com/vete-l/p/7063285.html>

## 4. 在网页中启动APP
 参考链接：<https://www.jianshu.com/p/1cd02fe1810f>
 
## 5. Android 中序列画的方式由哪些，有什么区别
   序列化为 Serializable 和 Parcelable
      
   | 区别 | Serializable | Parcelable
   | ---|---
   | 所属API |JAVA API | Android SDK API
   | ---|---
   | 原理 | 序列化和反序列化过程需要大量的I/O操作 | 序列化和反序列化过程不需要大量的I/O操作
   | ---|---
   | 开销 | 开销大 | 开销小
   | 效率 | 底 | 很高
   | 使用场景 | 序列化到本地或者通过网络传输 | 内存序列化
    
## 6. 性能优化时怎么做的

## 7. 如何控制进程的使用内存

## 8. http的数据结构

## 9. Android 和 JS的交互

## 10. 延时加载大图的方式

## 11. Token验证的方式

## 12. MediaPlay 播放音乐，连续切歌卡顿如何处理

## 13. Fragment 懒加载实现

## 14. 为什么 Android 规定不能在子线程中更新UI

## 15. Java 锁的使用方法

## 16. 对称加密和非对称加密的区别

## 17. 电商APP复杂首页怎么实现，都有什么方法

## 18. 如何避免OOM

## 19. Android 如何计算一个图片所占用的内存的
