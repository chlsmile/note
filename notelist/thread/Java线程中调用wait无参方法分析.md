## Java线程中调用wait无参方法分析
> 当调用对象的wait()方法后，线程会进入到WAITING状态，释放持有的锁，需要持有锁后才能够调用wait()方法

#### 示例代码
```java
import java.text.SimpleDateFormat;
import java.util.Date;

public class WaitTest {

    private final static SimpleDateFormat DATETIME_FORMAT=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");

    private final static Object lock=new Object();
    public static void main(String[] args) {
        Thread t1=new Thread(new Runnable() {
            @Override
            public void run() {
                synchronized (lock){
                    System.out.println("Thread t1 get lock success and sleep 10s "+DATETIME_FORMAT.format(new Date()));
                    try {
                        Thread.sleep(10000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println("Thread t1 sleep finished "+DATETIME_FORMAT.format(new Date()));
                    try {
                        System.out.println("Thread t1 begin wait "+DATETIME_FORMAT.format(new Date()));
                        lock.wait(); //当执行完lock.wait()后锁lock会被释放，其它线程能够获取锁
                        System.out.println("Thread t1 begin wait finished "+DATETIME_FORMAT.format(new Date()));
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println("Thread t1 finished "+DATETIME_FORMAT.format(new Date()));
                }
            }
        },"t1");
        t1.start();

        try {
            Thread.sleep(5000);//main线程sleep 5s 让上面的t1先获取lock
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        Thread t2=new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("t2线程尝试获取锁 "+DATETIME_FORMAT.format(new Date()));
                synchronized (lock){
                    System.out.println("t2线程获取锁成功 "+DATETIME_FORMAT.format(new Date()));
                    try {
                        System.out.println("t2线程开始sleep 40s "+DATETIME_FORMAT.format(new Date()));
                        Thread.sleep(40000); //执行sleep方法线程不会释放锁lock，待sleep结束后会释放锁
                        System.out.println("t2线程睡醒了 "+DATETIME_FORMAT.format(new Date()));
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        },"t2");
        t2.start();

        try {
            Thread.sleep(10000);//main线程sleep 10s 让上面的t2先获取锁
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        Thread t3=new Thread(new Runnable() {
            @Override
            public void run() {
                System.out.println("t3线程尝试获取锁 "+DATETIME_FORMAT.format(new Date()));
                synchronized (lock){
                    System.out.println("t3线程获取锁成功 "+DATETIME_FORMAT.format(new Date()));
                }
            }
        },"t3");

        t3.start();

        System.out.println("Thread main finished "+DATETIME_FORMAT.format(new Date()));
    }
}
```

#### 运行结果分析
![pic](https://github.com/chlsmile/note/blob/master/notefile/thread/java-wait-01.png)
![pic1](https://github.com/chlsmile/note/blob/master/notefile/thread/java-wait-02.png)
