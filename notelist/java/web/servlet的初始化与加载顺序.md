## Servlet的初始化与初始化顺序

### 一、Servlet的初始化
> Servlet可以通过两种方式进行初始化,容器启动的时候初始化(可以通过在web.xml中配置load-on-startup的值大于等于零来让容器启动的时候创建相应的Servlet),第一次被请求时候进行初始化.

#### 1.1容器启动时初始化
- 在web.xml中不配置load-on-startup,则容器启动时LifeDemoServlet的init方法不会执行;
- 在web.xml中配置load-on-startup的值小于0,则容器启动的时候LifeDemoServlet的init方法不会执行;
- 在web.xml中配置load-on-startup的值为大于等于0的值,则容器启动时LifeDemoServlet的init方法执行.

#### 1.2第一次使用时初始化
- 在web.xml中不配置load-on-startup,则在第一次请求LifeDemoServlet的时候LifeDemoServlet会进行初始化调用init方法.

#### 示例代码LifeDemoServlet类与web.xml文件如下:
```java
package com.chlsmile.demo.web;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Created with: IntelliJ IDEA.
 * Function:
 * User: chl_smile
 * Date: 2016-09-22 18:37:00
 */
public class LifeDemoServlet extends HttpServlet {

    public void init(ServletConfig config) throws ServletException{
        System.out.println("LifeDemoServlet init 方法执行了");
    }

    public void destroy(){
        System.out.println("LifeDemoServlet destroy 方法执行了");
    }

    public void service(HttpServletRequest req, HttpServletResponse resp){
        System.out.println("LifeDemoServlet service 方法执行了");
    }

}
```
```java
<!DOCTYPE web-app PUBLIC
        "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
        "http://java.sun.com/dtd/web-app_2_3.dtd" >

<web-app>
    <display-name>servlet demo web</display-name>
    <servlet>
        <servlet-name>LifeDemoServlet</servlet-name>
        <servlet-class>com.chlsmile.demo.web.LifeDemoServlet</servlet-class>
        <load-on-startup>0</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>LifeDemoServlet</servlet-name>
        <url-pattern>/LifeDemoServlet</url-pattern>
    </servlet-mapping>
</web-app>
```

### 二、Servlet的初始化顺序
- 在web.xml中定义了多个Servlet时,可以通过配置web.xml中的load-on-startup来指定初始化顺序(load-on-startup的值大于等于0),load-on-startup的数值越小则对应的Servlet越优先初始化.
- 如果多个Servlet的load-on-startup值相同,则这些Servlet的初始化顺序是由Servlet容器自己决定的,不会哪个Servlet在web.xml中的位置靠前就优先初始化.





