# 第6讲-SQL语言之概述  

## 600-本讲学习什么（2分38秒）及第6讲教学课件PDF  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318154835.png)

## 601-SQL语言概述（8分31秒）  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318155249.png)


## 602-利用SQL建立数据库(16分44秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318160928.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318161014.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318161032.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318161058.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318161129.png)
## 603-利用SQL进行基本查询(13分55秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318161209.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318164846.png)

当要查询既学过001课程又学过002课程的学生的学号时，我们可以使用SQL的交集操作来实现。下面是相应的SQL语句：

```sql
SELECT student_id
FROM course_enrollment
WHERE course_id = '001'
INTERSECT
SELECT student_id
FROM course_enrollment
WHERE course_id = '002';
```

这段SQL语句的含义是，首先从包含课程选课信息的表course_enrollment中选择学过001课程的学生的学号，然后取这部分学生和学过002课程的学生的学号做交集操作，最终得到既学过001课程又学过002课程的学生的学号集合。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318164948.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318165006.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240318165025.png)

SQL 通配符

通配符可用于替代字符串中的任何其他字符。

在 SQL 中，通配符与 SQL LIKE 操作符一起使用。

SQL 通配符用于搜索表中的数据。

在 SQL 中，可使用以下通配符：

| 通配符                                                       | 描述                       |
| ------------------------------------------------------------ | -------------------------- |
| %                                                            | 替代 0 个或多个字符        |
| _                                                            | 替代一个字符               |
| [_charlist_]                                                 | 字符列中的任何单一字符     |
| [^_charlist_]  <br>或  <br>[!_charlist_]                     | 不在字符列中的任何单一字符 |
|                                                              |                            |
| MySQL 中使用 **REGEXP** 或 **NOT REGEXP** 运算符 (或 RLIKE 和 NOT RLIKE) 来操作正则表达式。 |                            |

下面的 SQL 语句选取 name 以 "G"、"F" 或 "s" 开始的所有网站：

```sql
SELECT * FROM Websites  
WHERE name REGEXP '^[GFs]';
```

## 604-利用SQL进行多表联合查询(14分11秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319181917.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319182047.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319182141.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319184800.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319184822.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319184852.png)

要查询没学过李明老师课程的所有学生的学号，我们可以使用SQL的差集操作来实现。下面是相应的SQL语句：

```sql
SELECT student_id
FROM all_students
EXCEPT
SELECT student_id
FROM course_enrollment
WHERE teacher_name = '李明';
```

这段SQL语句的含义是，首先从包含所有学生信息的表all_students中选择所有学生的学号，然后从课程选课信息表course_enrollment中选择学过李明老师课程的学生的学号，最后取这两部分学生的学号集合做差集操作，得到所有没学过李明老师课程的学生的学号集合。
## 605-结合SELECT的INSERT语句(7分35秒)  

元组新增Insert：新增一个或一些元组到数据库的Table中

元组更新Update：对某些元组中的某些属性值进行重新设定

元组删除Delete：删除某些元组

SOL-DML既能单一记录操作，也能对记录集合进行批更新操作

SQL-DML之更新操作需要利用前面介绍的子查询（Subquery）的概念，以便处理“一些”、“某些”等。

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319201313.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319201343.png)

## 606-结合SELECT的DELETE与UPDATE语句(7分20秒)  


![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319201416.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319201441.png)



## 607-数据库定义的修正与撤销(4分55秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319201529.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240319201558.png)

撤消数据库

`drop database 数据库名；`

示例：撤消SCT数据库

`Drop database SCT;`

有些DBMS提供了操作多个数据库的能力，此时在进行数据库操作时需要指定待操作数据库与关闭数据库的功能

指定当前数据库

`use 数据库名；`

关闭当前数据库

`close 数据库名;`

## 第6讲模拟练习题  

易错点：

字符串型属性值需要加引号

“%”匹配零个或多个字符，所以不仅能匹配“张某某”也能匹配“张”和“张某”

7**有关系表SC ( S# , C#, Score)，求既学过“001”号课又学过 “002”号课的所有学生的学号，下列SQL语句正确的是`Select S1.S# From SC S1, SC S2 Where S1.S# = S2.S# and S1.C#=‘001’ and  S2.C#=‘002 ;`。**

17**已知关系S(S#,SN,AGE,SEX),SC(C#,S#,GRADE),C(C#,CN,TEACHER)。若要检索学生姓名及其选修课程的课程号和成绩，正确的SELECT语句是`SELECT S.SN,SC.C#,SC.GRADE FROM S,SC WHERE S.S#=SC.S#`。** （注意：这里要明确指出连接操作）

学得不好的点：

11**学生关系S（S#,Sname,Ssex,Sage,D#,Sclass）,S的属性分别表示学生的学号、姓名、性别、年龄。要在表S中删除一个属性“年龄”，可选用的SQL语句是`ALTER  TABLE  S  DROP  Sage`。**

15**查询结果输出时要求按“总评成绩”降序排列，相同者按“性别”升序，正确的子句是`ORDER BY 总评成绩 DESC,性别`。**