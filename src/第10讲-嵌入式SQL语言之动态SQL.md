# 第10讲-嵌入式SQL语言之动态SQL  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406145048.png)
## A00-本讲学习什么（1分15秒）及第10讲教学课件PDF  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406142136.png)

## A01-动态SQL的概念和作用（7分37秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406142330.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406142346.png)
## A02-动态SQL构造示例之一（15分41秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406142458.png)

## A03-动态SQL构造示例之二（16分17秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406142533.png)

## A04-动态SQL的两种执行方式（5分44秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406142639.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406142823.png)
## A05-数据字典及其作用（14分05秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406143037.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406143102.png)

模式的含义是指某一用户所设计和使用的表、索引及其他与数据库有关的对象的集
合，因此表的完整名应是：模式名.表名。这样做可允许不同用户使用相同的表名，而
不混淆。

一般而言，一个用户有一个模式。可以使用 Create schema 语句来创建模式（用法
略，参见相关文献），在 Create Table 等语句可以使用所定义的模式名称。

## A06-SQLDA与数据字典的应用（5分33秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406143433.png)

## A07-什么是ODBC（10分21秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406143605.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406143851.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406144044.png)
## A08-什么是JDBC（9分31秒）  

JDBC是什么？

JDBC:Java DataBase Connection

JDBC是一组Java版的应用程序接口API，提供了Java应用程序与数据库服务器的连接和通讯能力。

JDBC API

JDBC API分成两个程序包：

1、Java.sql 核心API--J2SE （Java2标准版）的一部分。使用java.sql.DriverManager类、java.sgl.Driver和Java.sql.connection接口连接到数据库

2、Javax.sql可选扩展API--J2EE（Java2企业版）的一部分。包含了基于JNDI（Java Naming and Directory Interface，Java命名和目录接口）的资源，以及管理连接池、分布式事务等，使用Datasource接口连接到数据库。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406144620.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406144717.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406144747.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406144852.png)


## A09-ODBC-JDBC-嵌入式之比较（10分22秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406144928.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406144953.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240406145012.png)

## 第10讲模拟练习题  


5、应用程序使用JDBC API访问数据库的具体实施过程有4步：

(3) 传递一个Driver给DriverManager，加载数据库驱动；

(1) 通过URL得到一个Connection对象, 建立数据库连接；

(2) 创建一个Statement对象(PreparedStatement或CallableStatement)，用来查询或者修改数据库；

(4) 执行查询并返回一个ResultSet，提取数据到应用程序。


9、SQLCA和SQLDA是嵌入在C语言中的SQL语言经常使用的两种数据结构。关于SQLCA和SQLDA，下列说法正确的是_________。

SQLCA是SQL通讯区，记录着SQL语句被DBMS执行后返回的状态信息；SQLDA是SQL描述区，记录着数据库/表等对象的定义信息。

10、应用程序通过ODBC连接一个数据库服务器的基本步骤如下：

(2)   SQLAllocConnect(env, &conn);

(1)   SQLConnect(conn, "aura.bell-labs.com", SQL_NTS, "avi", SQL_NTS, avipasswd", SQL_NTS);

(3)   { …. Do actual work … }

(4)   SQLDisconnect(conn)；SQLFreeConnect(conn)；SQLFreeEnv(env)；

11、关于嵌入式SQL语言的思维模式，说法正确的是_________。

建立数据库连接->声明一个游标(游标与SQL语句绑定)->打开游标(执行SQL语句)->循环地获取一条一条记录(属性与高级语言变量绑定)->关闭游标->可循环地再打开到关闭游标->断开数据库连接。

12、关于下面的思维模式，“建立数据库连接->请求分配语句句柄(申请内存空间)->用句柄执行SQL(句柄与SQL语句绑定)->建立高级语言变量与句柄属性的对应->循环地获取一条一条记录->释放语句句柄->断开数据库连接”。这是关于ODBC的思维模式。

13、关于下面的思维模式，“建立数据库连接->创建语句对象(申请内存空间)->用语句对象执行SQL(语句对象与SQL语句绑定)->返回结果对象->循环地从结果对象获取一条一条记录并提取对象的属性值传给高级语言变量->释放语句对象->断开数据库连接”。这是关于JDBC的思维模式。

14、SQL语句执行后，需要将结果记录集中的属性值，读到高级语言的变量中，那什么时候建立高级语言变量与属性的绑定，下列说法都正确。

嵌入式SQL语言：在一条一条地读取记录时(Fetch)建立绑定。

ODBC：在开始一条一条地读取记录之前用专门的语句建立绑定。

JDBC：一条一条记录的，边绑定，边读取相应的属性值。


16、一段构造SQL语句的程序代码如下：

```c
char *dcid, *acid, *ecid； 

dcid = “001”； ecid= “002”； acid= “003”；

strcpy(sqltext， “SELECT  *  from  Student  where  s# =”);

strcpy(sqltext，“: dcid”);

… …

exec sql whenever not found goto no_such_s#;

    exec sql prepare  ecid  from :sqltext;     

    exec sql execute  ecid  using :acid;    

    exec sql commit work;  continue;

 no_such_s#: printf("No such student in table Student\n");

    continue;
```

问：当该段程序执行“exec sql execute  ecid  using :acid;”语句时，其执行的查询是_______。

- A.检索001号同学的信息

- B.检索002号同学的信息

- C.检索003号同学的信息

- D.其他都不是

正确答案：C你错选为A


正确答案：C。解析：真正传给动态SOL语句的变量是acid，即检索003号同学的信息