## java中接口的特点

#### java中的接口存在两个特点
- 1.接口中定义的成员变量必须是由public static final来修饰的,编写源文件的时候可以省略这三个修饰词，编译成classes文件时会自动加上这三个修饰词;
- 2.接口中定义的方法必须是public abstract来修饰的,编写源文件的时候可以省略这两个修饰词，编译成classes文件时会自动加上这两个修饰词。

#### 源文件UserService接口示例
```java
public interface UserService {

    int                     a=10;
    static int              b=20;
    final  int              c=30;
    static final int        d=40;
    public static final int e=50;

    void addUser();

    public void updateUser();

    abstract void queryUser();

    public abstract void delUser();

}
```

#### 对源文件UserService进行编译，然后使用javap命令进行反编译查看结果(javap UserService)
```java
public interface com.chlsmile.demo.staticproxy.simple.UserService {
  public static final int a;
  public static final int b;
  public static final int c;
  public static final int d;
  public static final int e;
  public abstract void addUser();
  public abstract void updateUser();
  public abstract void queryUser();
  public abstract void delUser();
}
```

#### 对比总结
通过对源文件与使用javap进行反编译后对比可以发变量a,变量b,变量c,变量d在进行编译时都会变更为由public static final这三个关键词来修饰, 
addUser()方法,updateUser()方法,queryUser()方法最编译时都会变更为由public abstrac这两个关键词来修饰.


