1. create():创建一个完整的被观察者对象(Observable)
2. just():快速创建一个被观察者对象，并直接发送事件。最多只能发送10个参数。
3. fromArray():快速创建一个被观察者对象，并直接发送数组中的数据。会将数组中的数据转换为 Observable 对象。
4. fromIterable():快速创建一个被观察者对象，并直接发送集合中的数据。会将集合中的数据转换为 Observable 对象。
5. empty():快速创建一个被观察者对象，只调用 Complete 事件，直接通知完成。
6. error():快速创建一个被观察者对象，只调用 Error 事件，直接通知异常。可以自定义异常的类型。
7. never():快速创建一个被观察者对象，不发送任何事件。观察者接收后什么都不调用。
8. defer():有观察者订阅时，才会动态创建被观察者对象并且发送事件。
9. timer():快速创建一个被观察者对象，延迟指定时间后，发送一个数值0(Long 类型)，即延迟指定时间后调用了Next(0)。它默认是在一个新的线程里面，也可以为其指定调度器。timer(long,TimeUnit,Scheduler)
10. interval():快速创建一个被观察者对象，每隔指定的时间就发送事件。发送事件的顺序是从0开始，无限递增1的整数序列，直到取消订阅时停止发送。它默认是在computation调度器上执行，也可以为其指定调度器，interval(long,TimeUnit,Scheduler)。
11. intervalRange():快速创建一个被观察者对象，每隔指定的时间发送一个事件，可以指定发送的数量。发送事件的顺序是从0开始，无限递增1的整数序列，直到达到指定的数量停止发送。
12. range():快速创建一个被观察者对象，从指定数值开始发送指定数量的事件。发送事件的顺序是从0开始，无限递增1的整数序列，可以从指定数值开始。它与 intervalRange()的区别是事件没有延迟发送，是连续发送的。
13. rangeLong():类似 range(), 区别在于该方法支持的类型是 Long。
14. map():被观察者发送的事件都通过指定的函数处理，转换为另一种事件，即被观察者发送的事件转换为任意的事件类型。
15. flatMap():将被观察者发送的事件拆分、转换，在合并成一个新的事件序列传递给观察者。新合并生成的事件序列是无序的
16. concatMap():类似 flatMap(),只是新的事件序列和旧的事件序列顺序是相同的。
17. buffer():定期从被观察者对象获取定量的事件放入到缓存区中最终发送。
18. concat():组合多个被观察者一起发送数据，合并后 按发送顺序串行执行。
19. concatArray():和 concat() 类似，区别在于 concat() 组合的被观察者数量<=4,concatArray() 组合的被观察者数>4。
20. merge():组合多个被观察者一起发送，合并后按照时间线并行执行。
21. mergeArray():和 merge() 类似，区别在于 merge() 足组合的被观察数量<=4,mergeArray() 组合的被观察者数量>4。
22. concatDelayError():在使用 concat() 时，若其中的一个被观察者发出 onError 事件后，则马上中断其他被观察者发送事件，使用 concatDelayError() 作用是，等所有的被观察者事件发送结束后触发 onError()。
23. mergeDelayError():在使用 merge() 时，若其中的一个被观察者发出 onError 事件后，则马上中断其他被观察者发送事件，使用 mergeDelayError() 作用是，等所有的被观察者事件发送结束后触发 onError()。
24. zip():合并多个被观察者发送的对象，生成一个新的事件序列(合并后的时间序列)，并最终发送。事件的合并序列是按照原先的事件顺序，进行对位合并。最终合并的事件数量是多个被观察者中事件数量最少的数量。
25. combineLatest():当两个 Observables 中的任何一个发送了数据后，将先发送了数据的 Observables 的最新（最后）一个数据 与 另外一个 Observable 发送的每个数据结合，最终基于该函数的结果发送数据。
26. combineLatestDelayError():与 concatDelayError() /  mergeDelayError() 类似。
27. reduce():把被观察者需要发送的事件聚合成1个事件在发送，聚合的逻辑根据需求撰写，但本质都是前2个数据聚合，然后与后1个数据继续进行聚合，依次类推。
28. collect():将被观察者 Observable 发送的数据事件收集到一个集合里。
29. startWith():在一个被观察者发送事件前，追加发送一个数据或一个新的被观察者。
30. startWithArray():在一个被观察者发送事件前，追加发送多个数据或多个新的被观察者。
31. count():统计被观察者发送事件的数量。
32. subscribe():订阅，连接观察者和被观察者。
33. delay():使被观察者延迟发送事件。
34. do():在某个时间的声明周期中调用。
35. onErrorReturn():被观察者发送事件的过程中发生错误，发送一个特殊事件正常终止发送。
36. onErrorResumeNext():遇到错误的时候发送一个新的 Observable。onErrorResumeNext()拦截的错误是 Throwable，若需拦截 Exception 请用 onExceptionResumeNext(),若 onErrorResumeNext() 拦截的错误是 Exception，则会将错误传递给观察者的 onError 方法。
37. onExceptionResumeNext():遇到错误的时候发送一个新的 Observable。onExceptionResumeNext()拦截的错误是 Exception，若需拦截 Throwable 请用 onErrorResumeNext(),若 onExceptionResumeNext() 拦截的错误是 Throwable，则会将错误传递给观察者的 onError() 方法。
38. retry():重试，当出现错误的时候，让被观察者重新发送事件。
39. retryUntil():出现错误的时候，判断是否需要重新发送数据，返回 true 表示不发送。
40. retryWhen():遇到错误时，将发生的错误传递给一个新的被观察者，并决定是否需要重新订阅原始被观察者去发送事件。
41. repeat():无条件地、重复发送 被观察者事件。
42. repeatWhen():无条件地、重复发送 被观察者事件。
43. subscribeOn():指定被观察者的操作线程。指定多次，只有第一次生效。
44. observeOn():指定观察者的操作线程。
45. filter():过滤特定条件的事件，如果 test() 方法返回 true 表示发送，返回 false 表示不发送。
46. ofType():过滤指定数据类型的事件。如果是指定的类型代表发送，否则不发送。
47. skip():跳过某个事件，skip(1) 表示跳过第一个事件，skip(1, TimeUnit.SECONDS) 表示跳过第 1s 发送的事件。
48. skipLast():跳过某个事件，skipLast(2) 跳过最后两个事件，skipLast(1, TimeUnit.SECONDS) 跳过最后 1s 发送的事件。
49. distinct():跳过事件序列中重复的事件。
50. distinctUntilChanged():跳过事件序列中连续重复的事件。
51. take():指定观察者最多接收的事件。
52. takeLast():指定观察者只接受最后相应个数的事件。
53. throttFirst():发送指定时间内发送的第一个事件。
54. throttLast():发送指定时间内发送的最后一个事件。
55. sample():发送指定时间内发送的最后一个事件。与throttleLast() 类似。
56. throttleWithTimeout():发送数据事件时，若2次发送事件的间隔＜指定时间，就会丢弃前一次的数据，直到指定时间内都没有新数据发射时才会发送后一次的数据。
57. debounce():与throttleWithTimeout类似。
58. firstElement():选取事件队列中的第一个事件发送。
59. lastElement():选取事件队列中的最后一个事件发送。
60. elementAt():接收事件队列中指定索引的事件，索引从0开始，指定的最大索引可以大于事件队列的总数。
61. elementAtOrError():在 elementAt() 的基础上，当出现越界情况（即获取的位置索引 ＞ 发送事件序列长度）时，即抛出异常。
62. all():判断发送的每个数据是否满足设置的条件，如果满足返回 true，否则返回 false。
63. takeWhile():判断发送的每个数据是否满足是指的条件，如果满足发送数据，否则不发送。
64. skipWhile():判断发送的每个数据是否满足是指的条件，直到判断返回 false，才开始发送之后的数据。
65. takeUntil():发送的数据与判断条件返回 true时，停止发送事件。
66. skipUntil():等到 skipUntil() 传入的 Observable 开始发送数据，（原始）第1个 Observable 的数据才开始发送数据。
67. SequenceEqual():判断两个 Observable 发送的数据是否相同，如果相同返回 true，否则返回 false。
68. contains():判断发送的数据中是否有指定的数据，包含返回 true，否则返回 false。
69. isEmpty():判断发送的数据是否为空，是返回 true，否则返回 false。
70. amb():当需要发送多个 Observable 时，只发送 先发送数据的 Observable 的数据，而其余 Observable 则被丢弃。
71.  defaultIfEmpty():在不发送任何有效事件（ Next 事件）、仅发送了 Complete 事件的前提下，发送一个默认值.

**1~13 是创建操作符**

**14~17 是转换操作符**

**18~31 是合并操作符**

**32~44 是功能性操作符**

**45~61 是过滤操作符**

**62~71 是条件操作符**