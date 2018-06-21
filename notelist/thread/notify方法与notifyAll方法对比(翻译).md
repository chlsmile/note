## notify方法与notifyAll方法对比(翻译).md

http://javaconceptoftheday.com/difference-between-notify-and-notifyall-in-java/

> notify() and notifyAll() methods along with wait() method are used to establish a communication between the threads. A thread goes into WAITING mode by calling wait() method. This thread will be in WAITING state until any other thread calls either notify() or notifyAll() method on the same object. Look here how threads communicate with each other using wait(), notify() and notifyAll() in Java. Any thread calling wait(), notify() and notifyAll() must have lock of that object. In the other words, these methods must be called within synchronized method or synchronized block. In this post, we will see the differences between notify and notifyAll in Java with an example.


### notify() In Java :

When a thread calls notify() method on a particular object, only one thread will be notified which is waiting for the lock or monitor of that object. The thread chosen to notify is random i.e randomly one thread will be selected for notification. Notified thread doesn’t get the lock of the object immediately. It gets once the calling thread releases the lock of that object. Until that it will be in BLOCKED state. It will move from BLOCKED state to RUNNING state once it gets the lock.

Note : Before notification, the thread will be in WAITING state. Once it is notified, it will move to BLOCKED state. It remains in BLOCKED state until it gets the lock. Once it gets the lock, it moves from BLOCKED state to RUNNING state.

Let’s see notify() method with an example.
```java
class Shared
{
    synchronized void waitMethod()
    {
        Thread t = Thread.currentThread();
         
        System.out.println(t.getName()+" is releasing the lock and going to wait");
         
        try
        {
            wait();
        }
        catch (InterruptedException e) 
        {
            e.printStackTrace();
        }
         
        System.out.println(t.getName()+" has been notified and acquired the lock back");
    }
     
    synchronized void notifyOneThread()
    {
        Thread t = Thread.currentThread();
         
        notify();
         
        System.out.println(t.getName()+" has notified one thread waiting for this object lock");
    }
}
 
public class MainClass 
{   
    public static void main(String[] args) 
    {
        final Shared s = new Shared();
         
        //Thread t1 will be waiting for lock of object 's'
         
        Thread t1 = new Thread() 
        {
            @Override
            public void run()
            {
                s.waitMethod();
            }
        };
         
        t1.start();
         
        //Thread t2 will be waiting for lock of object 's'
         
        Thread t2 = new Thread() 
        {
            @Override
            public void run()
            {
                s.waitMethod();
            }
        };
 
        t2.start();
         
        //Thread t3 will be waiting for lock of object 's'
         
        Thread t3 = new Thread() 
        {
            @Override
            public void run()
            {
                s.waitMethod();
            }
        };
         
        t3.start();
         
        try
        {
            Thread.sleep(1000);
        } 
        catch (InterruptedException e) 
        {
            e.printStackTrace();
        }
         
        //Thread t4 will notify only one thread which is waiting for lock of object 's'
         
        Thread t4 = new Thread() 
        {
            @Override
            public void run()
            {
                s.notifyOneThread();
            }
        };
         
        t4.start(); 
    }    
}
```

output
```java
Thread-1 is releasing the lock and going to wait
Thread-0 is releasing the lock and going to wait
Thread-2 is releasing the lock and going to wait
Thread-3 has notified one thread waiting for this object lock
Thread-1 has been notified and acquired the lock back
```

### notifyAll() In Java :

When a thread calls notifyAll() method on a particular object, all threads which are waiting for the lock of that object are notified. All notified threads will move from WAITING state to BLOCKED state. All these threads will get the lock of the object on a priority basis. The thread which gets the lock of the object moves to RUNNING state. The remaining threads will remain in BLOCKED state until they get the object lock.

Below is an example of notifyAll() method in Java.

```java
class Shared
{
    synchronized void waitMethod()
    {
        Thread t = Thread.currentThread();
         
        System.out.println(t.getName()+" is releasing the lock and going to wait");
         
        try
        {
            wait();
        }
        catch (InterruptedException e) 
        {
            e.printStackTrace();
        }
         
        System.out.println(t.getName()+" has been notified and acquired the lock back");
    }
     
    synchronized void notifyAllThread()
    {
        Thread t = Thread.currentThread();
         
        notifyAll();
         
        System.out.println(t.getName()+" has notified all threads waiting for this object lock");
    }
}
 
public class MainClass 
{   
    public static void main(String[] args) 
    {
        final Shared s = new Shared();
         
        //Thread t1 will be waiting for lock of object 's'
         
        Thread t1 = new Thread() 
        {
            @Override
            public void run()
            {
                s.waitMethod();
            }
        };
         
        t1.start();
         
        //Thread t2 will be waiting for lock of object 's'
         
        Thread t2 = new Thread() 
        {
            @Override
            public void run()
            {
                s.waitMethod();
            }
        };
 
        t2.start();
         
        //Thread t3 will be waiting for lock of object 's'
         
        Thread t3 = new Thread() 
        {
            @Override
            public void run()
            {
                s.waitMethod();
            }
        };
         
        t3.start();
         
        try
        {
            Thread.sleep(1000);
        } 
        catch (InterruptedException e) 
        {
            e.printStackTrace();
        }
         
        //Thread t4 will notify all threads which are waiting for lock of object 's'
         
        Thread t4 = new Thread() 
        {
            @Override
            public void run()
            {
                s.notifyAllThread();
            }
        };
         
        t4.start(); 
    }    
}
```

Output:
```java
Thread-0 is releasing the lock and going to wait
Thread-2 is releasing the lock and going to wait
Thread-1 is releasing the lock and going to wait
Thread-3 has notified all threads waiting for this object lock
Thread-1 has been notified and acquired the lock back
Thread-2 has been notified and acquired the lock back
Thread-0 has been notified and acquired the lock back
```

### Difference Between notify And notifyAll In Java :
Below diagram summarizes the difference between notify and notifyAll in java.

![pic](https://github.com/chlsmile/note/blob/master/notefile/thread/NotifyVsNotifyAll.png)