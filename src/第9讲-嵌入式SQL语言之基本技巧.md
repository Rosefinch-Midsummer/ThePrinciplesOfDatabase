# 第9讲-嵌入式SQL语言之基本技巧  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190538.png)
## 900-本讲学习什么（1分47秒）及第9讲教学课件PDF  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407184740.png)
## 901-什么是嵌入式SQL语言（10分20秒）  

因此，高级语言+SQL语言：

既继承高级语言的过程控制性又结合SQL语言的复杂结果集操作的非过程性，同时又为数据库操作者提供安全可靠的操作方式：通过应用程序进行操作。

嵌入式SQL语言：

将SQL语言嵌入到某一种高级语言中使用。

这种高级语言，如C/C++，Java，PowerBuilder等，又称宿主语言（Host Language）

嵌入在宿主语言中的SQL与前面介绍的交互式SQL有一些不同的操作方式

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185058.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185116.png)

## 902-程序与数据库连接（6分35秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185241.png)

## 903-为什么需要提交和撤销（7分54秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185400.png)

## 904-嵌入式SQL程序的一个示例（5分50秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185513.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185537.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185554.png)

## 905-为什么需要游标（5分41秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185735.png)


![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185656.png)

游标是指向某检索记录集的指针

通过这个指针的移动，每次读一行，处理一行，再读一行...，直至处理完毕

游标（Cursor）的使用需要先定义、再打开（执行）、接着一条接一条处理，最后再关闭


## 906-游标应用示例（9分13秒）  



## 907-可滚动游标（4分22秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407185932.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190018.png)

可滚动游标移动时需判断是否到结束位置，或到起始位置

- 可通过判断是否到EOF位置（最后一条记录的后面），或BOF位置（起始记录的前面）
- 如果不需区分，可通过whenever not found语句设置来检测
## 908-利用游标进行数据库增删改（3分32秒）  



## 909-利用游标编写的一个程序（3分42秒）  



## 910-异常状态捕获机制（14分26秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190222.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190244.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190301.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190324.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190352.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190434.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190457.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240407190514.png)


## 第9讲模拟练习题  




21执行下面的程序：

```c
int main()

{   

	exec sql  whenever  sqlerror  goto  handle_error；
	
	exec sql  create table customers(cid  char(4)  not null, cname varchar(13), …)；
	
	…
	
	handle_error：
	
	exec sql drop customers；
	
	exec sql disconnect；
	
	fprintf(stderr,”could not create customers table\n”)；
	
	return -1；

}
```

如果customers表在执行过程中出现了问题，没有人为干预，则该程序“Exec sql drop customers；”语句将被执行的次数为无限。

解析：如果customers表在执行过程中出现问题，程序将跳转到handle_error标签并执行其中的代码。在handle_error标签中，程序会执行"exec sql drop customers"语句，然后再次跳转回handle_error标签。这样会导致无限循环执行该语句，因为每次执行后仍然会出现问题导致再次跳转到handle_error标签。所以，“exec sql drop customers；”语句将被执行的次数为无限次。





## 附录 C With MySQL

当使用C语言和MySQL进行联合处理时，通常会使用MySQL提供的C API（MySQL C API）来与数据库进行交互。通过这个API，可以在C语言中执行查询、获取结果集、插入记录等操作。

下面是一个简单的示例代码，演示如何使用C语言和MySQL进行联合处理：

```c
#include <stdio.h>
#include <mysql/mysql.h>

int main() {
    MYSQL *conn;
    MYSQL_RES *res;
    MYSQL_ROW row;

    conn = mysql_init(NULL);
    if (conn == NULL) {
        fprintf(stderr, "mysql_init() failed\n");
        return 1;
    }

    if (mysql_real_connect(conn, "localhost", "user", "password", "database", 0, NULL, 0) == NULL) {
        fprintf(stderr, "mysql_real_connect() failed\n");
        mysql_close(conn);
        return 1;
    }

    if (mysql_query(conn, "SELECT * FROM table")) {
        fprintf(stderr, "mysql_query() failed\n");
        mysql_close(conn);
        return 1;
    }

    res = mysql_store_result(conn);
    if (res == NULL) {
        fprintf(stderr, "mysql_store_result() failed\n");
        mysql_close(conn);
        return 1;
    }

    while ((row = mysql_fetch_row(res))) {
        printf("%s\n", row[0]);
    }

    mysql_free_result(res);
    mysql_close(conn);

    return 0;
}
```

在上面的代码中，我们首先初始化了一个MySQL连接，然后连接到指定的数据库，执行了一个SELECT查询，并打印查询结果中的第一列数据。

关于MySQL C API的更多信息和文档，你可以参考MySQL官方网站：[https://dev.mysql.com/doc/c-api/en/。](https://dev.mysql.com/doc/c-api/en/%E3%80%82)