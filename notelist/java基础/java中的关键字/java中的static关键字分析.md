##java中的static关键字分析

https://docs.oracle.com/javase/tutorial/java/javaOO/classvars.html

//是什么

//什么时候用

//怎么用

//静态属性,静态方法,静态代码块,静态类

当从同一个类创建多个对象时,每个对象都有自己独立的副本.例如一个汽车类Car,属性包括发动机engine,车轮wheel.每一个学生实例对象都有这些属性,并且存储于不同的内存空间.
有的时候你想有一个适用于所有实例对象的的变量.需要使用static关键字来实现.由static关键字来修改的变量称之为静态变量或者类变量.他们与类相关联而不与任何类关联.
类的每个实例对象都共享一个类变量,类变量存在于内存中一个固定的位置.任何一个类的实例对象都可以改变一个类变量的值,但类变量也可以不创建任何类的实例变量来操作.

例如,你想创建一批汽车对象并给每辆汽车都分配序列号,给第一个汽车对象标号为1,依次递增.每个对象的id号是唯一的,因此id是实例变量.
同时你想创建一个新的变量来记录已经创建了多少个汽车Car的实例来确定再创建一个新的汽车Car的实例变量id属性应该分配什么值.
这样的字段不应该与任何Car任何实例相关联,而应该是做为一个整体与类相关.你需要一个类变量numberOfCars,例如:
public class Car{
    private int id;
    private String engine;
    private String wheel;
    private static int numberOfCars;
}
类变量'通过类.变量名'方式引用,Car.numberOfCars,这能够清楚的表明numberOfCars变量是一个类变量
可以使用一个构造方法来设置id实例变量,并增加实例变量numberOfCars
public class Car{
    private int  id;
    private String engine;
    private String wheel;
    private static int numberOfCars;

    public Car(String engine, String wheel){
        this.engine=engine;
        this.wheel=wheel;
        id=++numberOfCars
    }

    public int getId(){
        return id;
    }
}


static关键字内存简单分析











