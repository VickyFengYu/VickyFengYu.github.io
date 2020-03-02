ReentrantLock vs Synchronized in Java
===================

ReentrantLock allow threads to enter into lock on a resource more than once. When the **thread first enters into lock, a hold count is set to one**. Before unlocking the thread can re-enter into lock again and every time hold count is incremented by one. For every unlock request, hold count is decremented by one and when hold count is 0, the resource is unlocked.

Reentrant Locks also offer a fairness parameter, by which the lock would abide by the order of the lock request i.e. after a thread unlocks the resource, the lock would go to the thread which has been waiting for the longest time. This fairness mode is set up by passing true to the constructor of the lock.


## <i class="icon-file"></i> ReentrantLock Methods

```
lock(): Call to the lock() method increments the hold count by 1 and gives the lock to the thread if the shared resource is initially free.

unlock(): Call to the unlock() method decrements the hold count by 1. When this count reaches zero, the resource is released.

tryLock(): If the resource is not held by any other thread, then call to tryLock() returns true and the hold count is incremented by one. If the resource is not free then the method returns false and the thread is not blocked but it exits.

tryLock(long timeout, TimeUnit unit): As per the method, the thread waits for a certain time period as defined by arguments of the method to acquire the lock on the resource before exiting.

lockInterruptibly(): This method acquires the lock if the resource is free while allowing for the thread to be interrupted by some other thread while acquiring the resource. It means that if the current thread is waiting for lock but some other thread requests the lock, then the current thread will be interrupted and return immediately without acquiring lock.

getHoldCount(): This method returns the count of the number of locks held on the resource.
isHeldByCurrentThread(): This method returns true if the lock on the resource is held by the current thread.
``` 

## <i class="icon-file"></i> Why use a ReentrantLock if one can use synchronized(this)

> A ReentrantLock is unstructured, unlike synchronized constructs -- i.e. you don't need to use a block structure for locking and can even hold a lock across methods. 

> Aside from that, ReentrantLock supports lock polling and interruptible lock waits that support time-out. ReentrantLock also has support for configurable fairness policy, allowing more flexible thread scheduling.

When should you use ReentrantLocks? According to that developerWorks article...

> The answer is pretty simple -- use it when you actually need something it provides that synchronized doesn't, like timed lock waits, interruptible lock waits, non-block-structured locks, multiple condition variables, or lock polling. ReentrantLock also has scalability benefits, and you should use it if you actually have a situation that exhibits high contention, but remember that the vast majority of synchronized blocks hardly ever exhibit any contention, let alone high contention. I would advise developing with synchronization until synchronization has proven to be inadequate, rather than simply assuming "the performance will be better" if you use ReentrantLock. Remember, these are advanced tools for advanced users. (And truly advanced users tend to prefer the simplest tools they can find until they're convinced the simple tools are inadequate.) As always, make it right first, and then worry about whether or not you have to make it faster.