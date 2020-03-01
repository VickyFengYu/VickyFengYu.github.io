# Python Lock and With


A primitive lock is a synchronization primitive that is not owned by a particular thread when locked. In Python, it is currently the lowest level synchronization primitive available, implemented directly by the _thread extension module.

- https://docs.python.org/3/library/threading.html.


## Locks


Locks are the most fundamental synchronization mechanism provided by the threading module. At any time, a lock can be held by a single thread, or by no thread at all. If a thread attempts to hold a lock that’s already held by some other thread, execution of the first thread is halted until the lock is released.

Locks are typically used to synchronize access to a shared resource. For each shared resource, create a Lock object. When you need to access the resource, call acquire to hold the lock (this will wait for the lock to be released, if necessary), and call release to release it:

```
lock = Lock()

lock.acquire() # will block if lock is already held
... access shared resource
lock.release()
```

For proper operation, it’s important to release the lock even if something goes wrong when accessing the resource. You can use try-finally for this purpose:

```
lock.acquire()
try:
    ... access shared resource
finally:
    lock.release() # release lock, no matter what
```

In Python 2.5 and later, you can also use the with statement. When used with a lock, this statement automatically acquires the lock before entering the block, and releases it when leaving the block:

from __future__ import with_statement # 2.5 only

```
with lock:
    ... access shared resource
The acquire method takes an optional wait flag, which can be used to avoid blocking if the lock is held by someone else. If you pass in False, the method never blocks, but returns False if the lock was already held:

if not lock.acquire(False):
    ... failed to lock the resource
else:
    try:
        ... access shared resource
    finally:
        lock.release()
```

You can use the locked method to check if the lock is held. Note that you cannot use this method to determine if a call to acquire would block or not; some other thread may have acquired the lock between the method call and the next statement.

```
if not lock.locked():
    # some other thread may run before we get
    # to the next line
    lock.acquire() # may block anyway
```
