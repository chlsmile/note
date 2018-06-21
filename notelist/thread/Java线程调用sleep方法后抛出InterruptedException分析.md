## Java线程调用sleep方法后抛出InterruptedException分析
> 如果在A线程中进行了sleep,那么可以在B线程中调用A线程的interrupt方法，促使A线程由TIMED_WAITING状态变更为RUNNABLE状态

#### 示例代码
```java

public class ThreadSleepTest {
    public static void main(String[] args) {
        Thread t1=new Thread(new Runnable() {
                @Override
                public void run() {
                System.out.println(Thread.currentThread().getName()+":开始执行...");
                try {
                    System.out.println("子线程开始睡20s");Thread.sleep(20000);
                } catch (InterruptedException e) {
                    System.out.println("子线被打断了");e.printStackTrace();
                }
                System.out.println(Thread.currentThread().getName()+":执行完了...");
            }
        },"子线程");
        t1.start();
        System.out.println("主线程开始执行");System.out.println("主线程睡5s");
        try {
            Thread.sleep(5000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("主线程睡醒了");
        t1.interrupt(); //中断子线程
    }
}
```

#### 代码运行分析
![pic](https://github.com/chlsmile/note/blob/master/notefile/thread/thread-sleep-interrupted-exception.png)