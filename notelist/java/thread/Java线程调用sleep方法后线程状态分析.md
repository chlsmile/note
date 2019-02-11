## Java线程调用sleep方法后线程状态分析
> 在java中调用线程的sleep方法会使线程进入到TIMED_WAITING状态

#### 示例代码
```java
public class ThreadSleepTest {

    public static void main(String[] args) {
        Thread t1=new Thread(new Runnable() {
            @Override
            public void run() {
            System.out.println(Thread.currentThread().getName()+":开始执行...");
            try {
                Thread.sleep(30000);//子线程sleep 30秒
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName()+":执行完了...");
            }
        },"子线程");
        t1.start();
        System.out.println("主线程执行完了");
    }
}
```

#### 代码运行线程状态分析
![pic](https://github.com/chlsmile/note/blob/master/notefile/thread/threadsleep.png)