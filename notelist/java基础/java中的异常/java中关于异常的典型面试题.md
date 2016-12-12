## java中关于异常的典型面试题

#### 面试题一

```java

public class Test {

    public int testException(){
        try{
            System.out.println("try block");
            System.exit(0);
        }catch (Exception e) {
            System.out.println("catch block");
        }finally{
            System.out.println("finally block");
        }
        return 0;
    }

    public static void main(String[] args) {
        Test t=new Test();
        System.out.println("result is:"+t.testException());
    }

}

```

#### 面试题一运行结果
```java
try block
```

#### 面试题一运行结果分析
> 由于System.exit(0)方法退出了虚拟机，所以finally中的代码块将不会执行


### 面试题二

```java

public class Test {

    public int testException() {
        try {
            return 0;
        } catch (Exception e) {
            System.out.println("catch block");
        } finally {
            System.out.println("finally block");
        }
        return 1;
    }

    public static void main(String[] args) {
        Test t = new Test();
        System.out.println("result is:"+t.testException());

    }
}

```

#### 面试题二运行结果
```java
finally block
result is:0
```

#### 面试题二运行结果分析
> 由于finally代码块中的语句一定会执行,所有虽然try代码块中进行了return,但finally中的语句还是会执行.finally中的内容虚拟机不退出就一定会执行,并且在return之前执行.

