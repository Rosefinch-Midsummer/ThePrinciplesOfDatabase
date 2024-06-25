# 第8讲-SQL语言与数据库完整性和安全性  



## 800-本讲学习什么（1分04秒）及第8讲教学课件PDF  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326143516.png)

## 801-数据库完整性概念及完整性约束规则(8分59秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326143552.png)

为什么会引发数据库完整性的问题呢？

- 不正当的数据库操作，如输入错误、操作失误、程序处理失误等

数据库完整性管理的作用

- 防止和避免数据库中不合理数据的出现
- DBMS应尽可能地自动防止DB中语义不合理现象
- 如DBMS不能自动防止，则需要应用程序员和用户在进行数据库操作时处处加以小心，每写一条SQL语句都要考虑是否符合语义完整性，这种工作负担是非常沉重的，因此应尽可能多地让DBMS来承担

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326143842.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326143905.png)


## 802-数据库完整性分类(4分16秒)  

一、按约束对象分类

域完整性约束条件：施加于某一列上，对给定列上所要更新的某一候选值是否可以接受进行约束条件判断，这是孤立进行的

关系完整性约束条件：施加于关系/table上，对给定table上所要更新的某一候选元组是否可以接受进行约束条件判断，或是对一个关系中的若干元组和另一个关系中的若干元组间的联系是否可以接受进行约束条件判断

二、按约束来源分类

结构约束：来自模型的约束，例如函数依赖约束、主键约束（实体完整性）、外键约束（参照完整性），只关心数值相等与否、是否允许空值等；

内容约束：来自用户的约束，如用户自定义完整性，关心元组或属性的取值范围。例如Student表的Sage属性值在15岁至40岁之间等

三、按约束状态分类

静态约束：要求DB在任一时候均应满足的约束；例如Sage在任何时候都应满足大于0而小于150（假定人活最大年龄是150）。

动态约束：要求DB从一状态变为另一状态时应满足的约束；例如工资只能升，不能降：工资可以是800元，也可以是1000元；可以从800元更改为1000元，但不能从1000元更改为800元

## 803-SQL表完整性与列完整性(21分11秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326144513.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326144533.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326144601.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326144628.png)

**check中的条件可以是Select-From-Where内任何Where后的语句，包含子查询。**

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326144802.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326144833.png)
## 804-SQL的断言及其应用(4分50秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326144854.png)

## 805-SQL的触发器的概念(6分34秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326152429.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326152501.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326152521.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326152545.png)


## 806-触发器应用示例之一(7分32秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326152613.png)


## 807-触发器应用示例之二(5分29秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326152652.png)

## 808-第8讲回顾本讲学习了什么-完整性回顾(1分51秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326152711.png)

## 809-数据库安全性的概念(6分06秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220018.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220055.png)

DBA的责任和义务
- 熟悉相关的法规、政策，协助组织的决策者制定好相关的安全策略
- 规划好安全控制保障措施，例如，系统安全级别、不同级别上的安全控制措施，对安全遭破坏的响应,
- **划分好数据的安全级别以及用户的安全级别**
- 实施安全性控制：DBMS专门提供一个DBA账户，该账户是一个超级用户或称系统用户。DBA利用该账户的特权可以进行用户账户的创建以及权限授予和撤消、安全级别控制调整等

## 810-自主安全性机制(10分55秒)  

自主安全性机制

- 通常情况下，自主安全性是通过授权机制来实现的。
- 用户在使用数据库前必须由DBA处获得一个账户，并由DBA授予该账户一定的权限，该账户的用户依据其所拥有的权限对数据库进行操作；同时，该帐户用户也可将其所拥有的权利转授给其他的用户(账户)，由此实现权限在用户之间的传播和控制。

授权者：决定用户权利的人

授权：授予用户访问的权利

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220425.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220456.png)

## 811-两种自主安全性控制(5分22秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220527.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220550.png)



## 812-SQL安全性控制(6分44秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220618.png)

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220702.png)

授予视图访问的权利，并不意味着授予基本表访问的权利(两个级别：基本关系级别和视图级别）

授权者授予的权利必须是授权者已经拥有的权利

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220804.png)

## 813-自主安全性控制的问题(3分56秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220832.png)

## 814-强制安全性机制(4分51秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220900.png)

DBMS引入强制安全性机制,可以通过扩展关系模式来实现

关系模式: R(A1: D1, A2: D2, ..., An:Dn)

对属性和元组引入安全性分级特性或称分类特性

R(A1: D1, C1, A2: D2, C2..., An:Dn, Cn, TC)

其中 C1,C2,..,Cn分别为属性D1,D2,..,Dn的安全分类特性; TC为元组的分类特性

这样,关系中的每个元组，都将扩展为带有安全分级的元组

强制安全性机制使得关系形成为多级关系(不同级别用户所能看到的关系的子集)，也出现多重实例、多级关系完整性等许多新的问题或新的处理技巧,在使用中需注意仔细研究。
## 815-第8讲回顾本讲学习了什么-安全性回顾(1分56秒)  

![](https://cdn.jsdelivr.net/gh/Rosefinch-Midsummer/MyImagesHost02/img/20240326220942.png)

## 第8讲模拟练习题  

在数据库的安全性控制中，授权的数据对象的范围越小，授权子系统就越灵活。