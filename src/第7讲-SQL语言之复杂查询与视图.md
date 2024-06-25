# 第7讲-SQL语言之复杂查询与视图  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325152118.png)

## 700-本讲学习什么（1分25秒）及第7讲教学课件PDF  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325121911.png)

## 701-IN子查询(11分47秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325132439.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325132525.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325132623.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325132725.png)


## 702-ThetaSome子查询(12分53秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325132755.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325132828.png)

为什么不用 Theta-any？

在SQL标准中，也有 Theta-any 谓词，但由于其语义的模糊性：any，“任一”是指所有呢？还是指某一个？不清楚，所以被 Theta-some 替代以求更明晰。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325133058.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325133132.png)

## 703-Exists子查询(11分48秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325133209.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325133257.png)

当在 SQL 中使用 IN 和 EXISTS 时，它们的主要区别在于它们的执行方式和用途。IN 子查询会将结果集与主查询进行比较，而 EXISTS 子查询只需检查子查询是否返回任何行即可。

下面是一个简单的示例来展示 IN 和 EXISTS 的区别：

使用 IN：

`SELECT *  FROM table1 WHERE column1 IN (SELECT column2 FROM table2);`

使用 EXISTS：

`SELECT *  FROM table1 t1 WHERE EXISTS (SELECT 1 FROM table2 t2 WHERE t1.column1 = t2.column2);`

关于 IN 和 EXISTS 的更多详细信息，请参考以下链接：

1. [IN vs EXISTS in SQL](https://www.geeksforgeeks.org/in-vs-exists-in-sql/)
2. [Difference between IN and EXISTS in S](https://www.sqlshack.com/difference-between-in-and-exists-in-sql-server/)

子查询表小的用in，子查询表大的用exists。

[从原理浅析MySQL中exists和in的区别（如何选用exists和in）](https://blog.csdn.net/taomeechildren/article/details/128922688)

但执行过程的区别在于：

exists子句会对外表（即t1）用loop逐条记录查询，每次查询都会查看exists中的select语句，如果select子句返回记录行（无论返回记录行是多少，只要能返回），exists就会返回true，则外表中的当前记录就会被检索出来；如果select子句没有返回记录行，exists就会返回false，则外表中的当前记录就会被丢弃。——exist子句循环每次取出外表中的一条记录用来执行exists中的语句查内表，是先查外表，再查内表（相关子查询）。

in查询相当于多个or条件的叠加。in子句需要先将子查询的记录全部查出来。注意in子句中的子查询返回的结果集必须只有一个字段。假设子查询返回的结果集有m条记录，在进行m次查询。——in子句是先执行in中的子句查出来内表的结果，然后外表针对内表查出来的结果一个个遍历匹配。即先查内表，再查外表（不相关子查询）。

基于以上的认识：

exists只有内表可以用上索引，外层循环必须要走一个遍历过程；而in内表和外表都可以用上索引，因为in本质上属于多个条件查询的并集(or)。

如何选用exists和in？

当两个表的大小相当时，用exists和in的效率差别不大。

如果两个表一个大一个小，则子查询表(即内表)大的用exists，子查询表(即内表)小的用in。
其实就是”小表驱动大表“的思想：用exist时外表是驱动表，用in时内表是驱动表。

MySQL的外连接就利用了”小表驱动大表“的思想做自动优化，因此有时候会发现LEFT JOIN左侧的不是驱动表而是被驱动表，其实就是MySQL优化器的功能。同理，内连接也有类似的情况。

## 704-结果计算与聚集计算(6分57秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325145109.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325145215.png)


## 705-分组聚集计算与分组过滤(10分38秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325145247.png)

GROUP BY 语句用于结合聚合函数，根据一个或多个列对结果集进行分组。

SQL GROUP BY 语法：

```sql
SELECT column_name, aggregate_function(column_name)  
FROM table_name  
WHERE column_name operator value  
GROUP BY column_name;
```

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325145340.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325145403.png)

在 SQL 中增加 HAVING 子句原因是，WHERE 关键字无法与聚合函数一起使用。

HAVING 子句可以让我们筛选分组后的各组数据。

SQL HAVING 语法：

```sql
SELECT column1, aggregate_function(column2) FROM table_name GROUP BY column1 HAVING condition;
```

**参数说明：**

- `column1`：要检索的列。
- `aggregate_function(column2)`：一个聚合函数，例如SUM、COUNT、AVG等，应用于`column2`的值。
- `table_name`：要从中检索数据的表。
- `GROUP BY column1`：根据`column1`列的值对数据进行分组。
- `HAVING condition`：一个条件，用于筛选分组的结果。只有满足条件的分组会包含在结果集中。


![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325145517.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325150027.png)
## 706-用SQL表达并交差操作(7分20秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325150138.png)

UNION运算符是Entry-SQL92的一部分

INTERSECT、EXCEPT运算符是Full-SQL92的一部分

它们都是Core-SQL99的一部分，但有些DBMS并不支持这些运算，使用时要注意

## 707-用SQL处理空值(3分53秒)  

空值是其值不知道、不确定、不存在的值

数据库中有了空值，会影响许多方面，如影响聚集函数运算的正确性，不能参与算术、比较或逻辑运算等

例如：右下图所示表SC，如果有某一记录为空值，则求001号课程的平均成绩？会是多少呢？

以前，很多DBMS将空值按默认值处理，如字符串类型则以空格来表示，而如数值类型则以0来表示，这也将会引起统计、计算上的不正确性。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325150440.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325150519.png)

## 708-用SQL表达连接与外连接操作(5分35秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325150550.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325150613.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325150655.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325150840.png)
## 709-SQL-SELECT小结(4分28秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325151207.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325151224.png)

面向对象/对象关系数据库的查询SQL→OQL

基本的SQL：另一SELECT-FROM-WHERE只能出现在WHERE子句；

新标准：引入对象概念，可以在能使用聚集（collection）的任何位置使用SELECT-FROM-WEHRE

FROM子句中使用

SELECT子句中使用

Where子句中使用

注意：本课程要求基本的 SQL
## 710-SQL视图(14分17秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325151505.png)

SQL数据库结构

- 基本表是实际存储于存储文件中的表，基本表中的数据是需要存储的
- 视图在SQL中只存储其由基本表导出视图所需要的公式，即由基本表产生视图的映像信息，不存储其数据，而是在运行过程中动态产生与维护
- 对视图数据的更改最终要反映在对基本表的更改上

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325151656.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325151726.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325151800.png)

可更新的视图是指可以对其进行插入、更新、删除操作的视图，这种视图通常基于单一表或多个表的简单查询结果构建而成，例如只包含一张表或者包含多张表但是通过 join 操作将其连接在一起的视图。在对可更新的视图进行操作时，系统会自动反映到视图所基于的表上。

不可更新的视图是指不能对其进行插入、更新、删除操作的视图，这种视图通常基于复杂的查询结果或包含特定计算、聚合、分组等操作的结果。例如，包含 group by 子句、distinct 子句、计算列、集合运算等的视图通常是不可更新的。在对不可更新的视图进行操作时，系统会提示更新失败或抛出错误信息。

总的来说，可更新的视图一般是简单的、基于单表或多表的连接查询，而不可更新的视图一般是复杂的、包含特定操作或计算结果的查询。

已经定义的视图也可以撤消

撤消视图

`Drop View Viewname`

当某一视图删除后，由该视图导出的其它视图也将自动删除

不仅视图可以撤消，基本表、数据库等都可以撤消

撤消基本表

`Drop Table 表名`
## 第7讲模拟练习题  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240325150138.png)

这个问题需要理解SQL中的集合运算符（如EXCEPT，UNION，INTERSECT）的工作方式。下面是对四个选项的解释：

“子查询1 Except 子查询2”返回在子查询1中出现但不在子查询2中出现的元组。

“子查询1 Union 子查询2”返回在子查询1和子查询2中出现的所有元组，但重复的元组只会出现一次。

“子查询1 Except ALL 子查询2”返回在子查询1中出现但不在子查询2中出现的元组，但是这个运算会考虑重复的元组。

“子查询1 Intersect 子查询2”返回同时在子查询1和子查询2中出现的元组。

31**假设一个元组在子查询1中出现m次，在子查询2中出现n次，其中m>0,n>0, 则下列说法正确的是____ ____。**

- A.该元组在“子查询1  Except  子查询2”中出现0次；

- B.该元组在“子查询1  Union  子查询2”中出现m + n次；

- C.该元组在 “子查询1  Except  ALL  子查询2”中出现m – n次；

- D.该元组在“子查询1  Intersect  子查询2”中出现min(m,n)次；

正确答案：A你错选为D

A.（正确答案）解析：Except是集合操作，出现0次

B.（错误答案）解析：此选项不正确。Union是集合操作，需去掉重复的元组

C.（错误答案）解析：此选项不正确。ExceptALL是包的操作，但应出现max（0，m-n）

D.（错误答案）解析：此选项不正确。Intersect是集合运算，只能出现一次。


32**假设一个元组在子查询1中出现m次，在子查询2中出现n次，其中m>0,n>0,则下列说法正确的是_________。**

- A.该元组在“子查询1  Union  ALL 子查询2”中出现m + n次；

- B.该元组在 “子查询1 Union  子查询2”中出现m+n次；

- C.该元组在“子查询1  Union  ALL 子查询2”中出现1次；

- D.该元组在 “子查询1 Union  子查询2”中出现min(m,n)次；

正确答案：A你选对了

A.（正确答案）解析：此选项正确。UnionALL是包的操作，应出现m+n次

B.（错误答案）解析：此选项不正确。Union是集合的操作，应去掉重复的元组

C.（错误答案）解析：此选项不正确。UnionALL是包的操作，不应去掉重复的元组

D.（错误答案）解析：此选项不正确。Union是集合的操作，只能出现一次

33**假设一个元组在子查询1中出现m次，在子查询2中出现n次，其中m>0,n>0,则下列说法正确的是_________。**

- A.该元组在“子查询1  Except  子查询2”中出现0次；

- B.该元组在“子查询1  Union  子查询2”中出现m + n次；

- C.该元组在 “子查询1  Except All 子查询2”中出现m – n次；

- D.该元组在“子查询1  Union All  子查询2”中出现max(m,n)次；

正确答案：A你错选为B

A.（正确答案）解析：此选项正确

B.（错误答案）解析：此选项不正确。Union是集合操作，只能出现一次

C.（错误答案）解析：此选项不正确。ExceptALL是包的操作，可出现`max(0, m-n)`次

D.（错误答案）解析：此选项不正确。UnionALL是包操作，出现m+n次。

40**有一个学生表student，包含主键S#（学生编号）等。又有分数表SC，包含S#（学生编号）、score（分数）等。已知student表中共有50个学生，有45人参加了考试（分数存在SC表中），其中10人不及格。执行以下SQL语句：select * from student where exists (select S# from SC where score<60 )， 可返回多少条记录？**

A.（正确答案）解析：此选项正确。因为这是非相关子查询，而且子查询始终为真（因为已
知有10人不及格），故检索出的是Student表中的所有记录

该SQL语句的结构使用了子查询和EXISTS关键字，这是一个半连接查询。它的意义是：如果子查询（select S# from SC where score<60）返回的结果集不为空，那么主查询就会执行。这里的子查询是查找SC表中分数小于60的学生编号，根据题目，有10名学生不及格，所以子查询的结果集肯定不为空。

**然而，这个SQL语句的问题是，子查询并未与主查询产生直接的关联。即，主查询并不会因为子查询返回的S#而过滤结果。当EXISTS子查询返回真（即，存在至少一个满足条件的记录时），主查询就会返回所有记录**。

所以，执行这个SQL语句将返回student表中所有的记录，即返回**50条记录**。