
Semaphore
===================


## <i class="icon-file"></i> Semaphore in Python

[https://docs.python.org/3/library/threading.html](https://docs.python.org/3/library/threading.html)

A semaphore manages an internal counter which is decremented by each acquire() call and incremented by each release() call. The counter can never go below zero; when acquire() finds that it is zero, it blocks, waiting until some other thread calls release().

There are many cases we may want to allow more than one worker access to a resource while still limiting the overall number of accesses.


## <i class="icon-file"></i> Semaphore in Java

Java provide Semaphore class in **java.util.concurrent package** that implements this mechanism.


### <i class="icon-file"></i> Constructors in Semaphore class

```
Semaphore(int num)
Semaphore(int num, boolean how)
```

Here, num specifies the initial permit count. Thus, it specifies the number of threads that can access a shared resource at any one time. If it is one, then only one thread can access the resource at any one time. By default, all waiting threads are granted a permit in an undefined order. By setting how to true, you can ensure that waiting threads are granted a permit in the order in which they requested access.


### <i class="icon-file"></i> Working of Semaphore

In general, to use a semaphore, the thread that wants access to the shared resource tries to acquire a permit.


If the semaphore’s count is greater than zero, then the thread acquires a permit, which causes the semaphore’s count to be decremented.
Otherwise, the thread will be blocked until a permit can be acquired.
When the thread no longer needs an access to the shared resource, it releases the permit, which causes the semaphore’s count to be incremented.
If there is another thread waiting for a permit, then that thread will acquire a permit at that time.


### <i class="icon-file"></i> Flow Chart

![enter image description here](https://github.com/VickyFengYu/VickyFengYu.github.io/blob/master/image/java/semaphore-flow-chart.jpeg?raw=true)
