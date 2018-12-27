### Servlet
Servlet技术的核心是Servlet，它是所有Servlet类必须直接或间接实现的一个接口。

Servlet接口定义了Servlet与Servlet容器之间的契约。这个契约归结起来就是，Servlet容器将Servlet类载入内存，并在Servlet实例上调用具体的方法。在一个应用程序中，每种Servlet类型只能有一个实例。

Servlet接口中定义了以下5个方法：
```java
void init(ServletConfig config) throws ServletException;
void service(ServletRequest req, ServletResponse res) throws ServletException, IOException;
void destroy();
String getServletInfo();
ServletConfig getServletConfig();
```
init、service和destroy是生命周期方法。Servlet容器根据以下规则调用这3个方法：
* init，当该Servlet第一次被请求时，Servlet容器会调用这个方法。这个方法在后续请求中不会再被调用。我们可以利用这个方法执行相应初始化工作。调用这个方法时，Servlet容器会传入一个ServletConfig。一般来说，你会将ServletConfig赋给一个类级变量，因此这个对象可以通过Servlet类的其他点来使用。
* service，每当请求Servlet时，Servlet容器就会调用这个方法。编写代码时，是假设Servlet要在这里被请求。第一次请求Servlet时，Servlet容器调用init方法和service方法。后续的请求将只调用service方法。
* destroy，当要销毁Servlet时，Servlet容器就会调用这个方法。当要卸载应用程序，或者当要关闭Servlet容器时，就会发生这种情况。一般会在这个方法中编写清除代码。


Servlet中的另外两个方法是非生命周期方法，即getServletInfo和getServletConfig：
* getServletInfo，这个方法会返回Servlet的描述。你可以返回有用或为null的任意字符串。
* getServletConfig，这个方法会返回由Servlet容器传给init方法的ServletConfig。但是，为了让getServletConfig返回一个非null值，必须将传给init方法的ServletConfig赋给一个类级变量。

注意线程安全性。Servlet实例会被一个应用程序中的所有用户共享，因此不建议使用类级变量，除非它们是只读的，或者是java.util.concurrent.atomic包的成员。


