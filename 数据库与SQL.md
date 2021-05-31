数据库与SQL

[TOC]



通过命令行进入MySQL

```mysql
mysql -hlocalhost -uroot -p
```

退出MySQL

```mysql
exit
```

查看你所有的数据库

```mysql
show databases
```

查看表结构

```mysql
describe <表名>
```

------



## 一、初识数据库

数据库（Database，DB）：数据库是将大量数据保存起来，通过计算机加工而成的可以 进行高效访问的数据集合。该数据集合称为数据库（Database，DB）

==数据库管理系统（Database Management System，DBMS）==：用来管理数据库的计算机系统

### 1.1 DBMS的种类

主要通过数据的保存格式（数据库的种类）分类，5种类型

- 层次数据库（Hierarchical Database，HDB）
- 关系数据库（Relational Database，RDB）

这种类型的 DBMS 称为==关系数据库管理系统==（Relational Database Management System，==RDBMS==）。比较具有代表性的 RDBMS 有如下 5 种。

```
* Oracle Database：甲骨文公司的RDBMS
* SQL Server：微软公司的RDBMS
* DB2：IBM公司的RDBMS
* PostgreSQL：开源的RDBMS
* MySQL：开源的RDBMS
```

- 面向对象数据库（Object Oriented Database，OODB）
- XML数据库（XML Database，XMLDB）
- 键值存储系统（Key-Value Store，KVS），举例：MongoDB

### 1.2 RDBMS的常见系统结构

最常见：客户端 / 服务器类型（C/S类型）

![img](https://img.alicdn.com/imgextra/i2/O1CN01kROUDI22ITX6Evayf_!!6000000007097-0-tps-567-333.jpg)

## 二、初识SQL

### 2.1 概念介绍

![img](https://img.alicdn.com/imgextra/i3/O1CN01zD5lrT1CMGnR7oQpa_!!6000000000066-0-tps-601-353.jpg)

实际使用的 SQL 语句当中有 90% 属于 DML

DML（Data Manipulation Language，数据操纵语言） 用来查询或者变更表中的记录。DML 包含以下几种指令。

- SELECT ：查询表中的数据
- INSERT ：向表中插入新数据
- UPDATE ：更新表中的数据
- DELETE ：删除表中的数据

### 2.2 SQL的基本书写规则

- SQL语句要以分号（ ; ）结尾
- SQL 不区分关键字的大小写，但是插入到表中的数据是区分大小写的
- 单词需要用半角空格或者换行来分隔

### 2.3 数据库的创建（CREATE DATABASE 语句）

语法：

```mysql
CREATE DATABASE < 数据库名称 > ;
```

例子：商品库

```mysql
CREATE DATABASE shop;
```

### 2.4 表的创建（CREATE TABLE 语句）

==注意：在创建表前要注明使用的数据库==

```mysql
use < 数据库名称 > ;
```

语法：

```mysql
CREATE TABLE < 表名 >
( < 列名 1> < 数据类型 > < 该列所需约束 > ,
  < 列名 2> < 数据类型 > < 该列所需约束 > ,
  < 列名 3> < 数据类型 > < 该列所需约束 > ,
  < 列名 4> < 数据类型 > < 该列所需约束 > ,
  .
  .
  .
  < 该表的约束 1> , < 该表的约束 2> ,……);
```

例子：商品表

```mysql
CREATE TABLE product(
     product_id CHAR(4) NOT NULL, 
     product_name VARCHAR(100) NOT NULL, 
     product_type VARCHAR(32) NOT NULL, 
     sale_price INTEGER, 
     purchase_price INTEGER, 
     regist_date DATE, 
     PRIMARY KEY(product_id)
 )  ;
```

### 2.5 命名规则

- 只能使用半角英文字母、数字、下划线（_）作为数据库、表和列的名称
- 名称必须以半角英文字母开头

商品表和product 表列名的对应关系

![img](https://img.alicdn.com/imgextra/i2/O1CN01Rf1px41ttjCsSRlAc_!!6000000005960-2-tps-592-276.png)

### 2.6 数据类型的指定

数据库创建的表，所有的列都必须指定数据类型，每一列都不能存储与该列数据类型不符的数据

四种最基本的数据类型：

| 数据类型   | 介绍                                                         |
| ---------- | ------------------------------------------------------------ |
| INTEGER 型 | 用来指定存储整数的列的数据类型（数字型），不能存储小数。     |
| CHAR 型    | 用来存储定长字符串，当列中存储的字符串长度达不到最大长度的时候，使用半角空格进行补足，由于会浪费存储空间，所以一般不使用。 |
| VARCHAR 型 | 用来存储可变长度字符串，定长字符串在字符数未达到最大长度时会用半角空格补足，但可变长字符串不同，即使字符数未达到最大长度，也不会用半角空格补足。 |
| DATE 型    | 用来指定存储日期（年月日）的列的数据类型（日期型）。         |

### 2.7 约束的设置

约束是除了数据类型之外，对列中存储的数据进行限制或者追加条件的功能。

`NOT NULL`是非空约束，即该列必须输入数据。

`PRIMARY KEY`是主键约束，代表该列是唯一值，可以通过该列取出特定的行的数据。

### 2.8 表的删除和更新

- 删除表的语法：删除的表是无法恢复的，只能重新插入，请执行删除操作时无比要谨慎。

```mysql
DROP TABLE < 表名 > ;
```

- 添加列（字段）的 ALTER TABLE 语句

```mysql
ALTER TABLE < 表名 > ADD COLUMN < 列的定义 >;
```

- 删除列的 ALTER TABLE 语句：执行之后无法恢复。误添的列可以通过 ALTER TABLE 语句删除，或者将表全部删除之后重新再创建

```mysql
ALTER TABLE < 表名 > DROP COLUMN < 列名 >;
```

【扩展内容】

- 清空表内容：相比`drop``/``delete`，`truncate`用来清除数据时，速度最快

```mysql
TRUNCATE TABLE TABLE_NAME;
```

- 数据的更新

基本语法：

```
UPDATE <表名>
SET <列名> = <表达式> [, <列名2>=<表达式2>...];  
WHERE <条件>;  -- 可选，非常重要。
ORDER BY 子句;  --可选
LIMIT 子句; --可选
```

**使用 update 时要注意添加 where 条件，否则将会将所有的行按照语句修改**

```
-- 修改所有的注册时间
UPDATE product
   SET regist_date = '2009-10-10';  
-- 仅修改部分商品的单价
UPDATE product
   SET sale_price = sale_price * 10
 WHERE product_type = '厨房用具';  
```

使用 UPDATE 也可以将列更新为 NULL（该更新俗称为NULL清空）。此时只需要将赋值表达式右边的值直接写为 NULL 即可。

```
-- 将商品编号为0008的数据（圆珠笔）的登记日期更新为NULL  
UPDATE product
   SET regist_date = NULL
 WHERE product_id = '0008';  
```

和 INSERT 语句一样， UPDATE 语句也可以将 NULL 作为一个值来使用。
**但是，只有未设置 NOT NULL 约束和主键约束的列才可以清空为NULL。**如果将设置了上述约束的列更新为 NULL，就会出错，这点与INSERT 语句相同。

多列更新

```
UPDATE product
   SET sale_price = sale_price * 10,
       purchase_price = purchase_price / 2
 WHERE product_type = '厨房用具';  
```

### 2.9 向product表中插入数据

基本语法

```
INSERT INTO <表名> (列1, 列2, 列3, ……) VALUES (值1, 值2, 值3, ……);  
```

对表进行全列 INSERT 时，可以省略表名后的列清单。这时 VALUES子句的值会默认按照从左到右的顺序赋给每一列。

```mysql
-- 包含列清单
INSERT INTO productins (product_id, product_name, product_type, 
sale_price, purchase_price, regist_date) VALUES ('0005', '高压锅', '厨房用具', 6800, 5000, '2009-01-15');
-- 省略列清单
INSERT INTO productins 
VALUES ('0005', '高压锅', '厨房用具', 6800, 5000, '2009-01-15');  
```

原则上，执行一次 INSERT 语句会插入一行数据。插入多行时，通常需要循环执行相应次数的 INSERT 语句。其实很多 RDBMS 都支持一次插入多行数据。

```mysql
-- 多行INSERT （ DB2、SQL、SQL Server、 PostgreSQL 和 MySQL多行插入）
INSERT INTO productins VALUES ('0002', '打孔器', 
'办公用品', 500, 320, '2009-09-11'),
('0003', '运动T恤', '衣服', 4000, 2800, NULL),
('0004', '菜刀', '厨房用具', 3000, 2800, '2009-09-20'); 
```

INSERT 语句中想给某一列赋予 NULL 值时，可以直接在 VALUES子句的值清单中写入 NULL。想要插入 NULL 的列一定不能设置 NOT NULL 约束。

向表中插入默认值（初始值），可以通过在创建表的 CREATE TABLE 语句中设置 **DEFAULT** 约束来设定默认值。

```mysql
CREATE TABLE productins
(product_id CHAR(4) NOT NULL,
（略）
sale_price INTEGER
（略）	DEFAULT 0, -- 销售单价的默认值设定为0;
PRIMARY KEY (product_id));
```

可以使用 INSERT...SELECT 语句从其他表复制数据。

```mysql
-- 将商品表中的数据复制到商品复制表中
INSERT INTO productocpy (product_id, product_name, product_type, sale_price, purchase_price, regist_date)
SELECT product_id, product_name, product_type, sale_price, 
purchase_price, regist_date
FROM Product;  
```

------

SQL 基础查询与排序

##  一、SELECT语句基础

### 1.1 从表中选取数据

**SELECT 语句**

从表中选取数据时需要使用SELECT语句，也就是只从表中选出（SELECT）必要数据的意思。通过SELECT语句查询并选取出必要数据的过程称为匹配查询或查询。

```
SELECT <列名>,
  FROM <表名>;
```

### 1.2 从表中选取符合条件的数据

**WHERE 语句**

SELECT 语句通过WHERE子句来指定查询数据的条件。在WHERE 子句中可以指定“某一列的值和这个字符串相等”或者“某一列的值大于这个数字”等条件。执行含有这些条件的SELECT语句，就可以查询出只符合该条件的记录了。

```
SELECT <列名>, ……
  FROM <表名>
 WHERE <条件表达式>;
```

```mysql
mysql> SELECT regist_date, product_type
    -> FROM product
    -> WHERE product_type = '衣服';
+-------------+--------------+
| regist_date | product_type |
+-------------+--------------+
| 2021--0-19  | 衣服         |
+-------------+--------------+

mysql> SELECT regist_date
    -> FROM product
    -> WHERE product_type = '衣服';
+-------------+
| regist_date |
+-------------+
| 2021--0-19  |
+-------------+
```

### 1.3 相关法则

- 星号（*）代表全部列的意思。
- SQL中可以随意使用换行符，不影响语句执行（但不可插入空行）。
- 设定汉语别名时需要使用双引号（"）括起来。
- 在SELECT语句中使用DISTINCT可以删除重复行。
- 注释是SQL语句中用来标识说明或者注意事项的部分。分为1行注释"-- "和多行注释两种"/* */"。

```mysql
-- 想要查询出全部列时，可以使用代表所有列的星号（*）。
SELECT *
  FROM <表名>;
  
mysql> SELECT *
    -> FROM product;
+------------+-------------+--------------+------------+
| product_id | regist_date | product_type | sale_price |
+------------+-------------+--------------+------------+
| 0009       | 2021-04-19  | 衣服         | 300        |
| 0007       | 2021-03-03  | 电脑         | 9000       |
| 0008       | 2021-04-09  | 电脑         | 8000       |
+------------+-------------+--------------+------------+

-- SQL语句可以使用AS关键字为列设定别名（用中文时需要双引号（“”））。
SELECT product_id     AS id,
       product_name   AS name,
       purchase_price AS "进货单价"
  FROM product;

mysql> SELECT product_id AS id,
    -> regist_date AS date,
    -> product_type AS type,
    -> sale_price AS "进货单价"
    -> FROM product;
+------+------------+------+----------+
| id   | date       | type | 进货单价 |
+------+------------+------+----------+
| 0009 | 2021-04-19 | 衣服 | 300      |
| 0007 | 2021-03-03 | 电脑 | 9000     |
| 0008 | 2021-04-09 | 电脑 | 8000     |
+------+------------+------+----------+
  
-- 使用DISTINCT删除product_type列中重复的数据
SELECT DISTINCT product_type
  FROM product;

mysql> SELECT DISTINCT product_type
    -> FROM product;
+--------------+
| product_type |
+--------------+
| 衣服         |
| 电脑         |
+--------------+
```

## 二、算术运算符和计较运算符

### 2.1 算术运算符

SQL语句中可以使用的四则运算的主要运算符如下：

| 含义 | 运算符 |
| ---- | ------ |
| 加法 | +      |
| 减法 | -      |
| 乘法 | *      |
| 除法 | /      |

### 2.2 比较运算符

SQL常见比较运算符如下：

| 运算符 | 含义      |
| ------ | --------- |
| =      | 和~相等   |
| <>     | 和~不相等 |
| \>=    | 大于等于  |
| \>     | 大于~     |
| \<=    | 小于等于~ |
| \<     | 小于~     |

### 2.3 常用法则

- SELECT子句中可以使用常数或者表达式。
- 使用比较运算符时一定要注意不等号和等号的位置。
- 字符串类型的数据原则上按照字典顺序进行排序，不能与数字的大小顺序混淆。
- 希望选取NULL记录时，需要在条件表达式中使用IS NULL运算符。希望选取不是NULL的记录时，需要在条件表达式中使用IS NOT NULL运算符。

```mysql
-- SQL语句中也可以使用运算表达式
SELECT product_name, sale_price, sale_price * 2 AS "sale_price x2"
  FROM product;
-- WHERE子句的条件表达式中也可以使用计算表达式
SELECT product_name, sale_price, purchase_price
  FROM product
 WHERE sale_price-purchase_price >= 500;
/* 对字符串使用不等号
首先创建chars并插入数据
选取出大于‘2’的SELECT语句*/
-- DDL：创建表
CREATE TABLE chars
（chr CHAR（3）NOT NULL，
PRIMARY KEY（chr））;
-- 选取出大于'2'的数据的SELECT语句('2'为字符串)
SELECT chr
  FROM chars
 WHERE chr > '2';
-- 选取NULL的记录
SELECT product_name，purchase_price
  FROM product
 WHERE purchase_price IS NULL;
-- 选取不为NULL的记录
SELECT product_name，purchase_price
  FROM product
 WHERE purchase_price IS NOT NULL;
```

## 三、逻辑运算符

### 3.1 NOT运算符

想要表示“不是……”时，除了前文的<>运算符外，还存在另外一个表示否定、使用范围更广的运算符：NOT。

NOT不能单独使用，如下例：

```mysql
-- 选取出销售单价大于等于1000日元的记录
SELECT product_name, product_type, sale_price
  FROM product
 WHERE sale_price >= 1000;
 -- 向代码清单2-30的查询条件中添加NOT运算符
SELECT product_name, product_type, sale_price
  FROM product
 WHERE NOT sale_price >= 1000;
```

### 3.2 AND运算符和OR运算符



AND 相当于“并且”，类似数学中的取交集；

OR 相当于“或者”，类似数学中的取并集。

AND运算符工作效果图

![img](https://img.alicdn.com/imgextra/i2/O1CN01KFHgix1Lnay1mJisr_!!6000000001344-2-tps-733-378.png)

OR运算符工作效果图

![img](https://img.alicdn.com/imgextra/i2/O1CN01fAdYrN1aSj9qK2909_!!6000000003329-2-tps-740-387.png)

### 3.3 通过括号优先处理

如果要查找这样一个商品，该怎么处理？

> “商品种类为办公用品”并且“登记日期是 2009 年 9 月 11 日或者 2009 年 9 月 20 日”
> 理想结果为“打孔器”，但当你输入以下信息时，会得到错误结果

```sql
-- 将查询条件原封不动地写入条件表达式，会得到错误结果
SELECT product_name, product_type, regist_date
  FROM product
 WHERE product_type = '办公用品'
   AND regist_date = '2009-09-11'
    OR regist_date = '2009-09-20';
```

错误的原因是**是 AND 运算符优先于 OR 运算符**，想要优先执行OR运算，可以使用**括号**：

```sql
-- 通过使用括号让OR运算符先于AND运算符执行
SELECT product_name, product_type, regist_date
  FROM product
 WHERE product_type = '办公用品'
   AND ( regist_date = '2009-09-11'
        OR regist_date = '2009-09-20');
```

### 3.4 真值表

当碰到条件较复杂的语句时，理解语句含义并不容易，这时可以采用**真值表**来梳理逻辑关系。

**AND运算符**：两侧的真值都为真时返回真，除此之外都返回假。

**OR运算符**：两侧的真值只要有一个不为假就返回真，只有当其两侧的真值都为假时才返回为假。

**NOT运算符**：将真转换为假，假转换为真。

### 3.5 含有NULL时的真值

NULL的真值结果既不为真，也不为假，因为并不知道这样一个值。

这时真值是除了真假之外的第三种值——**不确定**（UNKNOWN）。一般的逻辑运算并不存在这第三种值。SQL 之外的语言也基本上只使用真和假这两种真值。与通常的逻辑运算被称为二值逻辑相对，只有 SQL 中的逻辑运算被称为三值逻辑。

三值逻辑下的AND和OR真值表为：

**AND**

| P      | Q      | P AND Q |
| ------ | ------ | ------- |
| 真     | 真     | 真      |
| 真     | 假     | 假      |
| 真     | 不确定 | 不确定  |
| 假     | 真     | 假      |
| 假     | 假     | 假      |
| 假     | 不确定 | 假      |
| 不确定 | 真     | 不确定  |
| 不确定 | 假     | 假      |
| 不确定 | 不确定 | 不确定  |

**OR**

| P      | Q      | P OR Q |
| ------ | ------ | ------ |
| 真     | 真     | 真     |
| 真     | 假     | 真     |
| 真     | 不确定 | 真     |
| 假     | 真     | 真     |
| 假     | 假     | 假     |
| 假     | 不确定 | 不确定 |
| 不确定 | 真     | 真     |
| 不确定 | 假     | 不确定 |
| 不确定 | 不确定 | 不确定 |

**练习题**

请写出一条SELECT语句，从product表中选取出满足“销售单价打九折之后利润高于100日元的办公用品和厨房用具”条件的记录。查询结果要包括product_name列、product_type列以及销售单价打九折之后的利润（别名设定为profit）。

提示：销售单价打九折，可以通过saleprice列的值乘以0.9获得，利润可以通过该值减去purchase_price列的值获得。

```mysql
mysql> SELECT product_id, product_type, sale_price * 0.9 - purchase_price AS profit
    -> FROM product
    -> WHERE sale_price * 0.9 - purchase_price > 100 AND (product_type = '衣服' OR product_type = '电脑');
+------------+--------------+--------+
| product_id | product_type | profit |
+------------+--------------+--------+
| 0007       | 电脑         |    300 |
+------------+--------------+--------+
```

## 四、对表进行聚合查询

### 4.1 聚合函数

SQL中用于汇总的函数叫做聚合函数。以下五个是最常用的聚合函数：

| 函数名 | 介绍                         |
| ------ | ---------------------------- |
| COUNT  | 计算表中的记录数             |
| SUM    | 计算表中数值列中数据的合计值 |
| AVG    | 计算表中数值列中数据的平均值 |
| MAX    | 求出表中任意列中数据的最大值 |
| MIN    | 求出表中任意列中数据的最小值 |

```mysql
-- 计算全部数据的行数（包含NULL）
SELECT COUNT(*)
  FROM product;
-- 计算NULL以外数据的行数
SELECT COUNT(purchase_price)
  FROM product;
-- 计算销售单价和进货单价的合计值
SELECT SUM(sale_price), SUM(purchase_price) 
  FROM product;
-- 计算销售单价和进货单价的平均值
SELECT AVG(sale_price), AVG(purchase_price)
  FROM product;
-- MAX和MIN也可用于非数值型数据
SELECT MAX(regist_date), MIN(regist_date)
  FROM product;
```

### 4.2 使用聚合函数删除重复值

```mysql
-- 计算去除重复数据后的数据行数
SELECT COUNT(DISTINCT product_type)
 FROM product;
 
-- 是否使用DISTINCT时的动作差异（SUM函数）
SELECT SUM(sale_price), SUM(DISTINCT sale_price)
 FROM product;
```

### 4.3 常用法则

- COUNT函数的结果根据参数的不同而不同。COUNT(*)会得到包含NULL的数据行数，而COUNT(<列名>)会得到NULL之外的数据行数。
- 聚合函数会将NULL排除在外。但COUNT(*)例外，并不会排除NULL。
- MAX/MIN函数几乎适用于所有数据类型的列。SUM/AVG函数只适用于数值类型的列。
- 想要计算值的种类时，可以在COUNT函数的参数中使用DISTINCT。
- 在聚合函数的参数中使用DISTINCT，可以删除重复数据。

## 五、对表进行分组

### 5.1 GROUP BY 语句

```mysql
SELECT <列名1>,<列名2>, <列名3>, ……
  FROM <表名>
 GROUP BY <列名1>, <列名2>, <列名3>, ……;
```

```mysql
-- 按照商品种类统计数据行数
SELECT product_type, COUNT(*)
  FROM product
 GROUP BY product_type;
 
 mysql> SELECT product_type, COUNT(*)
    -> FROM product
    -> GROUP BY product_type;
+--------------+----------+
| product_type | COUNT(*) |
+--------------+----------+
| 衣服         |        1 |
| 电脑         |        2 |
+--------------+----------+

 -- 不含GROUP BY
SELECT product_type, COUNT(*)
  FROM product
  
 mysql> SELECT product_type, COUNT(*)
    -> FROM product;
ERROR 1140 (42000): In aggregated query without GROUP BY, expression #1 of SELECT list contains nonaggregated column 'shop.product.product_type'; this is incompatible with sql_mode=only_full_group_by
```

在 GROUP BY 子句中指定的列称为**聚合键**或者**分组列**

### 5.2 聚合键中包含NULL时

会将NULL作为一组特殊数据进行处理

```mysql
mysql> SELECT purchase_price, COUNT(*)
    -> FROM product
    -> GROUP BY purchase_price;
+----------------+----------+
| purchase_price | COUNT(*) |
+----------------+----------+
| 250            |        1 |
| 7800           |        1 |
| NULL           |        1 |
+----------------+----------+
```

### 5.3 GROUP BY 书写位置

GROUP BY的子句书写顺序有严格要求，不按要求会导致SQL无法正常执行，目前出现过的子句**书写顺序**为：

**1.SELECT → 2. FROM → 3. WHERE → 4. GROUP BY**

其中前三项用于筛选数据，GROUP BY对筛选出的数据进行处理

### 5.4 在WHERE子句中使用GROUP BY

```mysql
mysql> SELECT purchase_price, COUNT(*)
    -> FROM product
    -> WHERE product_type = '电脑'
    -> GROUP BY purchase_price;
+----------------+----------+
| purchase_price | COUNT(*) |
+----------------+----------+
| 7800           |        1 |
| NULL           |        1 |
+----------------+----------+
```

### 5.5 常见错误

在使用聚合函数及GROUP BY子句时，经常出现的错误有：

1. 在聚合函数的SELECT子句中写了聚合健以外的列 使用COUNT等聚合函数时，SELECT子句中如果出现列名，只能是GROUP BY子句中指定的列名（也就是聚合键）。

2. 在GROUP BY子句中使用列的别名 SELECT子句中可以通过AS来指定别名，但在GROUP BY中不能使用别名。因为在DBMS中 ,SELECT子句在GROUP BY子句后执行。

3. 在WHERE中使用聚合函数 原因是聚合函数的使用前提是结果集已经确定，而WHERE还处于确定结果集的过程中，所以相互矛盾会引发错误。 如果想指定条件，可以在SELECT，HAVING（下面马上会讲）以及ORDER BY子句中使用聚合函数。

## 六、为聚合结果指定条件

### 6.1 用HAVING得到特定分组

将表使用GROUP BY分组后，怎样才能只取出其中两组？

![å¾ç](https://img.alicdn.com/imgextra/i4/O1CN01vFuKi21OrfKkq4PfL_!!6000000001759-2-tps-497-442.png)

这里WHERE不可行，因为，WHERE子句只能指定记录（行）的条件，而不能用来指定组的条件

### 6.2 HAVING特点

HAVING子句用于对分组进行过滤，可以使用数字、聚合函数和GROUP BY中指定的列名（聚合键）。

```mysql
-- 数字
SELECT product_type, COUNT(*)
  FROM product
 GROUP BY product_type
HAVING COUNT(*) = 2;
-- 错误形式（因为product_name不包含在GROUP BY聚合键中）
SELECT product_type, COUNT(*)
  FROM product
 GROUP BY product_type
HAVING product_name = '圆珠笔';
```

## 七、对查询结果进行排序 

### 7.1 ORDER BY

```mysql
SELECT <列名1>, <列名2>, <列名3>, ……
  FROM <表名>
 ORDER BY <排序基准列1>, <排序基准列2>, ……
```

默认为升序排列，降序排列为DESC

```mysql
-- 降序排列
SELECT product_id, product_name, sale_price, purchase_price
  FROM product
 ORDER BY sale_price DESC;
 
 mysql> SELECT product_id, product_name, sale_price, purchase_price
    -> FROM product
    -> ORDER BY sale_price DESC;
+------------+--------------+------------+----------------+
| product_id | product_name | sale_price | purchase_price |
+------------+--------------+------------+----------------+
| 0005       | 高压锅       |       6800 |           5000 |
| 0003       | 运动T恤      |       4000 |           2800 |
| 0004       | 菜刀         |       3000 |           2800 |
| 0001       | T恤衫        |       1000 |            500 |
| 0007       | 擦菜板       |        880 |            790 |
| 0002       | 打孔器       |        500 |            320 |
| 0006       | 叉子         |        500 |           NULL |
| 0008       | 圆珠笔       |        100 |           NULL |
+------------+--------------+------------+----------------+

-- 多个排序键
SELECT product_id, product_name, sale_price, purchase_price
  FROM product
 ORDER BY sale_price, product_id;
 
 mysql> SELECT product_id, product_name, sale_price, purchase_price
    -> FROM product
    -> ORDER BY sale_price, product_id;
+------------+--------------+------------+----------------+
| product_id | product_name | sale_price | purchase_price |
+------------+--------------+------------+----------------+
| 0008       | 圆珠笔       |        100 |           NULL |
| 0002       | 打孔器       |        500 |            320 |
| 0006       | 叉子         |        500 |           NULL |
| 0007       | 擦菜板       |        880 |            790 |
| 0001       | T恤衫        |       1000 |            500 |
| 0004       | 菜刀         |       3000 |           2800 |
| 0003       | 运动T恤      |       4000 |           2800 |
| 0005       | 高压锅       |       6800 |           5000 |
+------------+--------------+------------+----------------+


-- 当用于排序的列名中含有NULL时，NULL会在开头或末尾进行汇总。
SELECT product_id, product_name, sale_price, purchase_price
  FROM product
 ORDER BY purchase_price;
 
 mysql> SELECT product_id, product_name, sale_price, purchase_price
    -> FROM product
    -> ORDER BY purchase_price;
+------------+--------------+------------+----------------+
| product_id | product_name | sale_price | purchase_price |
+------------+--------------+------------+----------------+
| 0006       | 叉子         |        500 |           NULL |
| 0008       | 圆珠笔       |        100 |           NULL |
| 0002       | 打孔器       |        500 |            320 |
| 0001       | T恤衫        |       1000 |            500 |
| 0007       | 擦菜板       |        880 |            790 |
| 0003       | 运动T恤      |       4000 |           2800 |
| 0004       | 菜刀         |       3000 |           2800 |
| 0005       | 高压锅       |       6800 |           5000 |
+------------+--------------+------------+----------------+
```

### 7.2 ORDER BY 中列名可使用别名

**FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY**

在ORDER BY 中可以使用别名，在GROUP BY 中不能使用别名。

**练习题：**

请编写一条SELECT语句，求出销售单价（sale_price列）合计值大于进货单价（purchase_price列）合计值1.5倍的商品种类。执行结果如下所示。

```
product_type | sum  | sum 
-------------+------+------
衣服         | 5000 | 3300
办公用品      |  600 | 320
```

![å¾ç](https://img.alicdn.com/imgextra/i4/O1CN01WYHzWW24NApR7jXCu_!!6000000007378-2-tps-662-175.png)

```mysql
mysql> SELECT product_type, SUM(sale_price),SUM(purchase_price)
    -> FROM product
    -> GROUP BY product_type
    -> HAVING SUM(sale_price)>SUM(purchase_price)*1.5;
+--------------+-----------------+---------------------+
| product_type | SUM(sale_price) | SUM(purchase_price) |
+--------------+-----------------+---------------------+
| 衣服         |            5000 |                3300 |
| 办公用品     |             600 |                 320 |
+--------------+-----------------+---------------------+
```

------

## TASK 03：复杂查询方法-视图、子查询、函数等

### 3.1 视图

#### 3.1.1 什么是视图

视图是一个虚拟的表，不同于直接操作数据表，视图是依据SELECT语句来创建的，操作视图时会根据创建视图的SELECT语句生成一张虚拟表，然后在这张虚拟表上做SQL操作。

#### 3.1.2 视图与表有什么区别

视图是基于真实表的一张虚拟的表，其数据来源均建立在真实表的基础上

视图不是表，视图是虚表，视图依赖于表

#### 3.1.3 为什么会存在视图

1. 可以将频繁使用的SELECT 语句保存以提高效率
2. 可以使用户看到的数据更加清晰
3. 可以不对外公开数据表全部字段，增强数据的保密性
4. 可以降低数据的冗余

#### 3.1.4 如何创建视图

创建视图的基本语法如下：

```mysql
CREATE VIEW <视图名称>(<列名1>,<列名2>,...) AS <SELECT语句>
```

SELECT 语句中列的排列顺序和视图中列的排列顺序相同

==视图名在数据库中需要是唯一的，不能与其他视图和表重名==

在一般的DBMS中定义视图时不能使用ORDER BY语句

- 基于单表的视图

```mysql
CREATE VIEW productsum (product_type, cnt_product)
AS
SELECT product_type, COUNT(*)
  FROM product
 GROUP BY product_type ;
 
 mysql> SELECT *
    -> FROM productSum;
+--------------+-------------+
| product_type | cnt_product |
+--------------+-------------+
| 衣服         |           2 |
| 办公用品     |           2 |
| 厨房用具     |           4 |
+--------------+-------------+
```

- 基于多表的视图

```mysql
CREATE VIEW view_shop_product(product_type, sale_price, shop_name)
AS
SELECT product_type, sale_price, shop_name
  FROM product,
       shop_product
 WHERE product.product_id = shop_product.product_id;
 
mysql> SELECT *
    -> FROM view_shop_product;
+--------------+------------+-----------+
| product_type | sale_price | shop_name |
+--------------+------------+-----------+
| 衣服         |       1000 | 东京      |
| 办公用品     |        500 | 东京      |
| 衣服         |       4000 | 东京      |
| 办公用品     |        500 | 名古屋    |
| 衣服         |       4000 | 名古屋    |
| 厨房用具     |       3000 | 名古屋    |
| 厨房用具     |        500 | 名古屋    |
| 厨房用具     |        880 | 名古屋    |
| 衣服         |       4000 | 大阪      |
| 厨房用具     |       3000 | 大阪      |
| 厨房用具     |        500 | 大阪      |
| 厨房用具     |        880 | 大阪      |
| 衣服         |       1000 | 福冈      |
+--------------+------------+-----------+
```

在视图的基础上查询

```mysql
mysql> SELECT sale_price, shop_name
    -> FROM view_shop_product
    -> WHERE product_type = '衣服';
+------------+-----------+
| sale_price | shop_name |
+------------+-----------+
|       1000 | 东京      |
|       4000 | 东京      |
|       4000 | 名古屋    |
|       4000 | 大阪      |
|       1000 | 福冈      |
+------------+-----------+
```

#### 3.1.5 如何修改视图结构

基本语法：

```mysql
ALTER VIEW <视图名> AS <SELECT语句>
```

```mysql
mysql> ALTER VIEW productSum
    -> AS
    -> SELECT product_type, sale_price
    -> FROM product
    -> WHERE regist_date > '2009-09-11';
    
 mysql> SELECT *
    -> FROM productSum;
+--------------+------------+
| product_type | sale_price |
+--------------+------------+
| 衣服         |       1000 |
| 厨房用具     |       3000 |
| 厨房用具     |        500 |
| 办公用品     |        100 |
+--------------+------------+
```

#### 3.1.6 如何更新视图内容

因为视图是一个虚拟表，所以对视图的操作就是对底层基础表的操作，所以在修改时只有满足底层基本表的定义才能成功修改。

我们在实际使用中尽量不通过修改视图来修改表

```mysql
mysql> UPDATE productSum
    -> SET sale_price = 5000
    -> WHERE product_type = '办公用品';
    
 mysql> SELECT *
    -> FROM productSum;
+--------------+------------+
| product_type | sale_price |
+--------------+------------+
| 衣服         |       1000 |
| 厨房用具     |       3000 |
| 厨房用具     |        500 |
| 办公用品     |       5000 |
+--------------+------------+
```

#### 3.1.7 如何删除视图

```mysql
DROP VIEW <视图名1> [ , <视图名2> …]

DROP VIEW productSum;
```

### 3.2 子查询

```mysql
SELECT stu_name
FROM (
         SELECT stu_name, COUNT(*) AS stu_cnt
          FROM students_info
          GROUP BY stu_age) AS studentSum;
```



#### 3.2.1 什么是子查询

子查询指一个查询语句嵌套在另一个查询语句内部的查询，在SELECT 语句中先计算子查询，子查询的结果作为外层另一个查询的过滤条件，查询可以基于一个表或者多个表。

#### 3.2.2 子查询和视图的关系

子查询就是将用来定义视图的 SELECT 语句直接用于 FROM 子句当中。其中AS studentSum可以看作是子查询的名称，而且由于子查询是一次性的，所以子查询不会像视图那样保存在存储介质中， 而是在 SELECT 语句执行之后就消失了。

#### 3.2.3 嵌套子查询

**虽然嵌套子查询可以查询出结果，但是随着子查询嵌套的层数的叠加，SQL语句不仅会难以理解而且执行效率也会很差，所以要尽量避免这样的使用。**

```mysql
SELECT product_type, cnt_product
FROM (SELECT *
        FROM (SELECT product_type, 
                      COUNT(*) AS cnt_product
                FROM product 
               GROUP BY product_type) AS productsum
       WHERE cnt_product = 4) AS productsum2;
       
 +--------------+-------------+
| product_type | cnt_product |
+--------------+-------------+
| 厨房用具     |           4 |
+--------------+-------------+
-- 其中最内层的子查询我们将其命名为productSum，这条语句根据product_type分组并查询个数，第二层查询中将个数为4的商品查询出来，最外层查询product_type和cnt_product两列。
```

#### 3.2.4 标量子查询

标量就是单一的意思，那么标量子查询也就是单一的子查询，要求我们执行的SQL语句只能返回一个值，也就是要返回表中具体的**某一行的某一列**

```mysql
-- 执行一次标量子查询后是要返回类似于，“0004”，“菜刀”这样的结果
product_id | product_name | sale_price 
------------+-------------+----------
0003       | 运动T恤       | 4000 
0004       | 菜刀          | 3000 
0005       | 高压锅        | 6800
```

#### 3.2.5 标量子查询有什么用

具体需求：

1. 查询出销售单价高于平均销售单价的商品
2. 查询出注册日期最晚的那个商品

```mysql
mysql> SELECT product_id, product_name, sale_price
    -> FROM product
    -> WHERE sale_price > (SELECT AVG(sale_price) FROM product);
+------------+--------------+------------+
| product_id | product_name | sale_price |
+------------+--------------+------------+
| 0003       | 运动T恤      |       4000 |
| 0004       | 菜刀         |       3000 |
| 0005       | 高压锅       |       6800 |
| 0008       | 圆珠笔       |       5000 |
+------------+--------------+------------+
```

```mysql
mysql> SELECT product_id, product_name, sale_price,(SELECT AVG(sale_price) FROM product) AS avg_price
    -> FROM product;
+------------+--------------+------------+-----------+
| product_id | product_name | sale_price | avg_price |
+------------+--------------+------------+-----------+
| 0001       | T恤衫        |       1000 | 2710.0000 |
| 0002       | 打孔器       |        500 | 2710.0000 |
| 0003       | 运动T恤      |       4000 | 2710.0000 |
| 0004       | 菜刀         |       3000 | 2710.0000 |
| 0005       | 高压锅       |       6800 | 2710.0000 |
| 0006       | 叉子         |        500 | 2710.0000 |
| 0007       | 擦菜板       |        880 | 2710.0000 |
| 0008       | 圆珠笔       |       5000 | 2710.0000 |
+------------+--------------+------------+-----------+
```

#### 3.2.6 关联子查询

- 什么是关联子查询

关联子查询就是通过一些标志将内外两层的查询连接起来起到过滤数据的目的

例子：

```mysql
mysql> SELECT product_type, product_name, sale_price
    -> FROM product AS p1
    -> WHERE sale_price > (SELECT AVG(sale_price) FROM product AS p2 WHERE p1.product_type = p2.product_type GROUP BY product_type);
+--------------+--------------+------------+
| product_type | product_name | sale_price |
+--------------+--------------+------------+
| 衣服         | 运动T恤      |       4000 |
| 厨房用具     | 菜刀         |       3000 |
| 厨房用具     | 高压锅       |       6800 |
| 办公用品     | 圆珠笔       |       5000 |
+--------------+--------------+------------+
```

- 关联子查询与子查询的联系

```mysql
-- 查询出销售单价高于平均销售单价的商品
SELECT product_id, product_name, sale_price
  FROM product
 WHERE sale_price > (SELECT AVG(sale_price) FROM product);
 
-- 选取出各商品种类中高于该商品种类的平均销售单价的商品
SELECT product_type, product_name, sale_price
  FROM product ASp1
 WHERE sale_price > (SELECT AVG(sale_price)
   FROM product ASp2
                      WHERE p1.product_type =p2.product_type
   GROUP BY product_type);
+--------------+--------------+------------+
| product_type | product_name | sale_price |
+--------------+--------------+------------+
| 衣服         | 运动T恤      |       4000 |
| 厨房用具     | 菜刀         |       3000 |
| 厨房用具     | 高压锅       |       6800 |
| 办公用品     | 圆珠笔       |       5000 |
+--------------+--------------+------------+
/* 
1.首先执行不带WHERE的主查询
2.根据主查询讯结果匹配product_type，获取子查询结果
3.将子查询结果再与主查询结合执行完整的SQL语句
*/
```

#### 练习题

1. 在视图中插入数据的同时也会在原表中插入数据，原表中有些列设置的不允许为空，可能会导致插入错误。
2. 请根据习题一中的条件编写一条 SQL 语句，创建一幅包含如下数据的视图（名称为AvgPriceByType）

```mysql
mysql> CREATE VIEW AvgPriceByType AS
    -> SELECT product_id, product_name,product_type,sale_price,
    -> (SELECT AVG(sale_price) FROM product AS p1 WHERE p1.product_type = p2.product_type GROUP BY product_type) AS avg_sale_price
    -> FROM product AS p2;
Query OK, 0 rows affected (0.03 sec)

mysql> SELECT *
    -> FROM AvgPriceByType;
+------------+--------------+--------------+------------+----------------+
| product_id | product_name | product_type | sale_price | avg_sale_price |
+------------+--------------+--------------+------------+----------------+
| 0001       | T恤衫        | 衣服         |       1000 |      2500.0000 |
| 0002       | 打孔器       | 办公用品     |        500 |      2750.0000 |
| 0003       | 运动T恤      | 衣服         |       4000 |      2500.0000 |
| 0004       | 菜刀         | 厨房用具     |       3000 |      2795.0000 |
| 0005       | 高压锅       | 厨房用具     |       6800 |      2795.0000 |
| 0006       | 叉子         | 厨房用具     |        500 |      2795.0000 |
| 0007       | 擦菜板       | 厨房用具     |        880 |      2795.0000 |
| 0008       | 圆珠笔       | 办公用品     |       5000 |      2750.0000 |
+------------+--------------+--------------+------------+----------------+
```

### 3.3 各种各样的函数

函数大致分为如下几类：

- 算术函数 （用来进行数值计算的函数）
- 字符串函数 （用来进行字符串操作的函数）
- 日期函数 （用来进行日期操作的函数）
- 转换函数 （用来转换数据类型和值的函数）
- 聚合函数 （用来进行数据聚合的函数）

#### 3.3.1 算术函数

- `+ - * /`四则运算在之前的章节介绍过，此处不再赘述
- ABS – 绝对值

ABS 函数用于计算一个数字的绝对值，表示一个数到原点的距离。

当 ABS 函数的参数为`NULL`时，返回值也是`NULL`。

- MOD – 求余数

MOD 是计算除法余数（求余）的函数，是 modulo 的缩写。小数没有余数的概念，只能对整数列求余数。

注意：主流的 DBMS 都支持 MOD 函数，只有SQL Server 不支持该函数，其使用`%`符号来计算余数。

- ROUND – 四舍五入

ROUND 函数用来进行四舍五入操作。

注意：当参数 **保留小数的位数** 为变量时，可能会遇到错误，请谨慎使用变量。

#### 3.3.2 字符串函数

- CONCAT – 拼接

语法：`CONCAT(str1, str2, str3)`

MySQL中使用 CONCAT 函数进行拼接。

- LENGTH – 字符串长度

语法：`LENGTH( 字符串 )`

- LOWER – 小写转换

LOWER 函数只能针对英文字母使用，它会将参数中的字符串全都转换为小写。该函数不适用于英文字母以外的场合，不影响原本就是小写的字符。

类似的， UPPER 函数用于大写转换。

- REPLACE – 字符串的替换

语法：`REPLACE( 对象字符串，替换前的字符串，替换后的字符串 )`

- SUBSTRING – 字符串的截取

语法：`SUBSTRING （对象字符串 FROM 截取的起始位置 FOR 截取的字符数）`

使用 SUBSTRING 函数 可以截取出字符串中的一部分字符串。截取的起始位置从字符串最左侧开始计算，索引值起始为1。

```mysql
mysql> SELECT str1,str2,str3,CONCAT(str1,str2,str3)AS str_concat, LENGTH(str1)AS  len_str1, LOWER(str1)AS low_str1, REPLACE(str1, str2, str3) AS rep_str, SUBSTRING(str1 FROM 3 FOR 2) AS sub_str
    -> FROM samplestr;
+-----------+------+------+-----------------+----------+-----------+-----------+---------+
| str1      | str2 | str3 | str_concat      | len_str1 | low_str1  | rep_str   | sub_str |
+-----------+------+------+-----------------+----------+-----------+-----------+---------+
| opx       | rt   | NULL | NULL            |        3 | opx       | NULL      | x       |
| abc       | def  | NULL | NULL            |        3 | abc       | NULL      | c       |
| 太阳      | 月亮 | 火星 | 太阳月亮火星    |        6 | 太阳      | 太阳      |         |
| aaa       | NULL | NULL | NULL            |        3 | aaa       | NULL      | a       |
| NULL      | xyz  | NULL | NULL            |     NULL | NULL      | NULL      | NULL    |
| @!#$%     | NULL | NULL | NULL            |        5 | @!#$%     | NULL      | #$      |
| ABC       | NULL | NULL | NULL            |        3 | abc       | NULL      | C       |
| aBC       | NULL | NULL | NULL            |        3 | abc       | NULL      | C       |
| abc哈哈   | abc  | ABC  | abc哈哈abcABC   |        9 | abc哈哈   | ABC哈哈   | c哈     |
| abcdefabc | abc  | ABC  | abcdefabcabcABC |        9 | abcdefabc | ABCdefABC | cd      |
| micmic    | i    | I    | micmiciI        |        6 | micmic    | mIcmIc    | cm      |
+-----------+------+------+-----------------+----------+-----------+-----------+---------+
```

- **（扩展内容）SUBSTRING_INDEX – 字符串按索引截取**

语法：`SUBSTRING_INDEX (原始字符串， 分隔符，n)`

该函数用来获取原始字符串按照分隔符分割后，第 n 个分隔符之前（或之后）的子字符串，支持正向和反向索引，索引起始值分别为 1 和 -1。

```mysql
-- 正向索引
mysql> SELECT SUBSTRING_INDEX('www.mysql.com', '.', 2);
+------------------------------------------+
| SUBSTRING_INDEX('www.mysql.com', '.', 2) |
+------------------------------------------+
| www.mysql                                |
+------------------------------------------+

-- 反向索引
mysql> SELECT SUBSTRING_INDEX('www.mysql.com','.',-2);
+-----------------------------------------+
| SUBSTRING_INDEX('www.mysql.com','.',-2) |
+-----------------------------------------+
| mysql.com                               |
+-----------------------------------------+
```

获取第1个元素比较容易，获取第2个元素/第n个元素可以采用二次拆分的写法。

```mysql
SELECT SUBSTRING_INDEX('www.mysql.com', '.', 1);
+------------------------------------------+
| SUBSTRING_INDEX('www.mysql.com', '.', 1) |
+------------------------------------------+
| www                                      |
+------------------------------------------+
1 row in set (0.00 sec)
SELECT SUBSTRING_INDEX(SUBSTRING_INDEX('www.mysql.com', '.', 2), '.', -1);
+--------------------------------------------------------------------+
| SUBSTRING_INDEX(SUBSTRING_INDEX('www.mysql.com', '.', 2), '.', -1) |
+--------------------------------------------------------------------+
| mysql                                                              |
+--------------------------------------------------------------------+
```

#### 3.3.3 日期函数

- CURRENT_DATE – 获取当前日期

```sql
SELECT CURRENT_DATE;
+--------------+
| CURRENT_DATE |
+--------------+
| 2020-08-08   |
+--------------+
1 row in set (0.00 sec)
```

- CURRENT_TIME – 当前时间

```sql
SELECT CURRENT_TIME;
+--------------+
| CURRENT_TIME |
+--------------+
| 17:26:09     |
+--------------+
1 row in set (0.00 sec)
```

- CURRENT_TIMESTAMP – 当前日期和时间

```sql
SELECT CURRENT_TIMESTAMP;
+---------------------+
| CURRENT_TIMESTAMP   |
+---------------------+
| 2020-08-08 17:27:07 |
+---------------------+
1 row in set (0.00 sec)
```

- EXTRACT – 截取日期元素

语法：`EXTRACT(日期元素 FROM 日期)`

使用 EXTRACT 函数可以截取出日期数据中的一部分，例如“年”

“月”，或者“小时”“秒”等。该函数的返回值并不是日期类型而是数值类型

```sql
SELECT CURRENT_TIMESTAMP as now,
EXTRACT(YEAR   FROM CURRENT_TIMESTAMP) AS year,
EXTRACT(MONTH  FROM CURRENT_TIMESTAMP) AS month,
EXTRACT(DAY    FROM CURRENT_TIMESTAMP) AS day,
EXTRACT(HOUR   FROM CURRENT_TIMESTAMP) AS hour,
EXTRACT(MINUTE FROM CURRENT_TIMESTAMP) AS MINute,
EXTRACT(SECOND FROM CURRENT_TIMESTAMP) AS second;
+---------------------+------+-------+------+------+--------+--------+
| now                 | year | month | day  | hour | MINute | second |
+---------------------+------+-------+------+------+--------+--------+
| 2020-08-08 17:34:38 | 2020 |     8 |    8 |   17 |     34 |     38 |
+---------------------+------+-------+------+------+--------+--------+
```

#### 3.3.4 转换函数

一是数据类型的转换，简称为类型转换，在英语中称为`cast`；另一层意思是值的转换。

- CAST – 类型转换

语法：`CAST（转换前的值 AS 想要转换的数据类型）`

```sql
-- 将字符串类型转换为数值类型
SELECT CAST('0001' AS SIGNED INTEGER) AS int_col;
+---------+
| int_col |
+---------+
|       1 |
+---------+
1 row in set (0.00 sec)
-- 将字符串类型转换为日期类型
SELECT CAST('2009-12-14' AS DATE) AS date_col;
+------------+
| date_col   |
+------------+
| 2009-12-14 |
+------------+
1 row in set (0.00 sec)
```

- COALESCE – 将NULL转换为其他值

语法：`COALESCE(数据1，数据2，数据3……)`

COALESCE 是 SQL 特有的函数。该函数会返回可变参数 A 中左侧开始第 1个不是NULL的值。参数个数是可变的，因此可以根据需要无限增加。

在 SQL 语句中将 NULL 转换为其他值时就会用到转换函数。

```sql
SELECT COALESCE(NULL, 11) AS col_1,
COALESCE(NULL, 'hello world', NULL) AS col_2,
COALESCE(NULL, NULL, '2020-11-01') AS col_3;
+-------+-------------+------------+
| col_1 | col_2       | col_3      |
+-------+-------------+------------+
|    11 | hello world | 2020-11-01 |
+-------+-------------+------------+
1 row in set (0.00 sec)
```

### 3.4 谓词

#### 3.4.1 什么是谓词

谓词就是返回值为真值的函数。包括`TRUE / FALSE / UNKNOWN`。

谓词主要有以下几个：

- LIKE
- BETWEEN
- IS NULL、IS NOT NULL
- IN
- EXISTS

#### 3.4.2 LIKE谓词 - 用于字符串的部分一致查询

部分一致大体可以分为前方一致、中间一致和后方一致三种类型

```sql
+--------+
| strcol |
+--------+
| abcdd  |
| abcddd |
| abddc  |
| abdddc |
| ddabc  |
| dddabc |
+--------+
```

- 前方一直：选取出“dddabc”

```sql
mysql> SELECT *
    -> FROM samplelike
    -> WHERE strcol LIKE 'ddd%';
+--------+
| strcol |
+--------+
| dddabc |
+--------+
```

其中的`%`是代表“零个或多个任意字符串”的特殊符号，本例中代表“以ddd开头的所有字符串”。

- 中间一致：选取出“abcddd”,“dddabc”,“abdddc”

中间一致即查询对象字符串中含有作为查询条件的字符串，无论该字符串出现在对象字符串的最后还是中间都没有关系。

```sql
SELECT *
FROM samplelike
WHERE strcol LIKE '%ddd%';
+--------+
| strcol |
+--------+
| abcddd |
| abdddc |
| dddabc |
+--------+
```

- 后方一致：选取出“abcddd“

```sql
SELECT *
FROM samplelike
WHERE strcol LIKE '%ddd';
+--------+
| strcol |
+--------+
| abcddd |
+--------+
```

- `_`下划线匹配任意 1 个字符

使用 _（下划线）来代替 %，与 % 不同的是，它代表了“任意 1 个字符”。

```sql
SELECT *
FROM samplelike
WHERE strcol LIKE 'abc__';
+--------+
| strcol |
+--------+
| abcdd  |
+--------+
```

#### 3.4.3 BETWEEN 谓词 - 用于范围查询

```sql
-- 选取销售单价为100～ 1000元的商品
SELECT product_name, sale_price
FROM product
WHERE sale_price BETWEEN 100 AND 1000;
+--------------+------------+
| product_name | sale_price |
+--------------+------------+
| T恤          |       1000 |
| 打孔器       |        500 |
| 叉子         |        500 |
| 擦菜板       |        880 |
| 圆珠笔       |        100 |
+--------------+------------+
```

BETWEEN 的特点就是结果中会包含 100 和 1000 这两个临界值，也就是**闭区间**。如果不想让结果中包含临界值，那就必须使用 < 和 >。

```sql
SELECT product_name, sale_price
FROM product
WHERE sale_price > 100
AND sale_price < 1000;
+--------------+------------+
| product_name | sale_price |
+--------------+------------+
| 打孔器       |        500 |
| 叉子         |        500 |
| 擦菜板       |        880 |
+--------------+------------+
```

#### 3.4.4 IS NULL、 IS NOT NULL - 用于判断是否为NULL

为了选取出某些值为 NULL 的列的数据，不能使用 =，而只能使用特定的谓词IS NULL。

```sql
SELECT product_name, purchase_price
FROM product
WHERE purchase_price IS NULL;
+--------------+----------------+
| product_name | purchase_price |
+--------------+----------------+
| 叉子         |           NULL |
| 圆珠笔       |           NULL |
+--------------+----------------+

SELECT product_name, purchase_price
FROM product
WHERE purchase_price IS NOT NULL;
+--------------+----------------+
| product_name | purchase_price |
+--------------+----------------+
| T恤          |            500 |
| 打孔器       |            320 |
| 运动T恤      |           2800 |
| 菜刀         |           2800 |
| 高压锅       |           5000 |
| 擦菜板       |            790 |
+--------------+----------------+
```

#### 3.4.5 IN谓词 - OR 的简便用法

多个查询条件取并集时可以选择使用`or`语句。

```sql
-- 通过OR指定多个进货单价进行查询
SELECT product_name, purchase_price
FROM product
WHERE purchase_price = 320
OR purchase_price = 500
OR purchase_price = 5000;
+--------------+----------------+
| product_name | purchase_price |
+--------------+----------------+
| T恤          |            500 |
| 打孔器       |            320 |
| 高压锅       |           5000 |
+--------------+----------------+
```

虽然上述方法没有问题，但还是存在一点不足之处，那就是随着希望选取的对象越来越多， SQL 语句也会越来越长，阅读起来也会越来越困难。这时， 我们就可以使用IN 谓词
`IN(值1, 值2, 值3, …)来替换上述 SQL 语句。

```sql
SELECT product_name, purchase_price
FROM product
WHERE purchase_price IN (320, 500, 5000);
+--------------+----------------+
| product_name | purchase_price |
+--------------+----------------+
| T恤          |            500 |
| 打孔器       |            320 |
| 高压锅       |           5000 |
+--------------+----------------+
```

反之，希望选取出“进货单价不是 320 元、 500 元、 5000 元”的商品时，可以使用否定形式NOT IN来实现。

```sql
SELECT product_name, purchase_price
FROM product
WHERE purchase_price NOT IN (320, 500, 5000);
+--------------+----------------+
| product_name | purchase_price |
+--------------+----------------+
| 运动T恤      |           2800 |
| 菜刀         |           2800 |
| 擦菜板       |            790 |
+--------------+----------------+
```

需要注意的是，==在使用IN 和 NOT IN 时是无法选取出NULL数据的==。
实际结果也是如此，上述两组结果中都不包含进货单价为 NULL 的叉子和圆珠笔。 NULL 只能使用 IS NULL 和 IS NOT NULL 来进行判断。

#### 3.4.6 使用子查询作为IN谓词的参数

假设我么需要取出大阪在售商品的销售单价，该如何实现呢？

第一步，取出大阪门店的在售商品 `product_id ;

第二步，取出大阪门店在售商品的销售单价 `sale_price

```sql
-- step1：取出大阪门店的在售商品 `product_id`
SELECT product_id
FROM shopproduct
WHERE shop_id = '000C';
+------------+
| product_id |
+------------+
| 0003       |
| 0004       |
| 0006       |
| 0007       |
+------------+

-- step2：取出大阪门店在售商品的销售单价 `sale_price`
SELECT product_name, sale_price
FROM product
WHERE product_id IN (SELECT product_id
  FROM shopproduct
                       WHERE shop_id = '000C');
+--------------+------------+
| product_name | sale_price |
+--------------+------------+
| 运动T恤      |       4000 |
| 菜刀         |       3000 |
| 叉子         |        500 |
| 擦菜板       |        880 |
+--------------+------------+

-- 子查询展开后的结果
SELECT product_name, sale_price
FROM product
WHERE product_id IN ('0003', '0004', '0006', '0007');
+--------------+------------+
| product_name | sale_price |
+--------------+------------+
| 运动T恤      |       4000 |
| 菜刀         |       3000 |
| 叉子         |        500 |
| 擦菜板       |        880 |
+--------------+------------+
```

既然 in 谓词也能实现，那为什么还要使用子查询呢？这里给出两点原因：

①：实际生活中，某个门店的在售商品是不断变化的，使用 in 谓词就需要经常更新 sql 语句，降低了效率，提高了维护成本；

②：实际上，某个门店的在售商品可能有成百上千个，手工维护在售商品编号真是个大工程。

使用子查询即可保持 sql 语句不变，极大提高了程序的可维护性，这是系统开发中需要重点考虑的内容。

- NOT IN和子查询

#### 3.4.7 EXIST 谓词

- EXIST 谓词的使用方法

谓词的作用就是 **“判断是否存在满足某种条件的记录”**。如果存在这样的记录就返回真（TRUE），如果不存在就返回假（FALSE）。EXIST（存在）谓词的主语是“记录”。

```sql
mysql> SELECT product_name, sale_price
    -> FROM product AS p
    -> WHERE EXISTS (SELECT * FROM shopproduct AS sp WHERE sp.shop_id = '000C' AND sp.product_id = p.product_id);
+--------------+------------+
| product_name | sale_price |
+--------------+------------+
| 运动T恤      |       4000 |
| 菜刀         |       3000 |
| 叉子         |        500 |
| 擦菜板       |        880 |
+--------------+------------+
```

- EXIST 的参数

 EXIST 是只有 1 个参数的谓词。 所以，EXIST 只需要在右侧书写 1 个参数，该参数通常都会是一个子查询。

EXIST 通常会使用关联子查询作为参数。

- 子查询中的SELECT *

大家可以把在 EXIST 的子查询中书写 SELECT * 当作 SQL 的一种习惯。

- 使用NOT EXIST 替换 NOT IN

就像 EXIST 可以用来替换 IN 一样， NOT IN 也可以用NOT EXIST来替换。

### 3.5 CASE 表达式

#### 3.5.1 什么是CASE表达式

语法：

```sql
CASE WHEN <求值表达式> THEN <表达式>
     WHEN <求值表达式> THEN <表达式>
     WHEN <求值表达式> THEN <表达式>
     .
     .
     .
ELSE <表达式>
END  
```

上述语句执行时，依次判断 when 表达式是否为真值，是则执行 THEN 后的语句，如果所有的 when 表达式均为假，则执行 ELSE 后的语句。
无论多么庞大的 CASE 表达式，最后也只会返回一个值。

#### 3.5.2 CASE表达式的使用方法

- 应用场景1：根据不同分支得到不同列值

```sql
SELECT  product_name,
        CASE WHEN product_type = '衣服' THEN CONCAT('A ： ',product_type)
             WHEN product_type = '办公用品'  THEN CONCAT('B ： ',product_type)
             WHEN product_type = '厨房用具'  THEN CONCAT('C ： ',product_type)
             ELSE NULL
        END AS abc_product_type
  FROM  product;
+--------------+------------------+
| product_name | abc_product_type |
+--------------+------------------+
| T恤          | A ： 衣服        |
| 打孔器       | B ： 办公用品    |
| 运动T恤      | A ： 衣服        |
| 菜刀         | C ： 厨房用具    |
| 高压锅       | C ： 厨房用具    |
| 叉子         | C ： 厨房用具    |
| 擦菜板       | C ： 厨房用具    |
| 圆珠笔       | B ： 办公用品    |
+--------------+------------------+
```

#### 3.5.2 CASE表达式的使用方法

- 应用场景2：实现列方向上的聚合

```sql
-- 对按照商品种类计算出的销售单价合计值进行行列转换
SELECT SUM(CASE WHEN product_type = '衣服' THEN sale_price ELSE 0 END) AS sum_price_clothes,
       SUM(CASE WHEN product_type = '厨房用具' THEN sale_price ELSE 0 END) AS sum_price_kitchen,
       SUM(CASE WHEN product_type = '办公用品' THEN sale_price ELSE 0 END) AS sum_price_office
  FROM product;
+-------------------+-------------------+------------------+
| sum_price_clothes | sum_price_kitchen | sum_price_office |
+-------------------+-------------------+------------------+
|              5000 |             11180 |              600 |
+-------------------+-------------------+------------------+
```

- 应用场景3：实现行转列

1. **当待转换列为数字时，可以使用**`SUM AVG MAX MIN`**等聚合函数；**

2. **当待转换列为文本时，可以使用**`MAX MIN`**等聚合函数**

![å¾ç](https://img.alicdn.com/imgextra/i1/O1CN01IMBZDB1q7gojkvNse_!!6000000005449-2-tps-219-136.png)

![å¾ç](https://img.alicdn.com/imgextra/i4/O1CN01If3OFs1SfXJOk69gs_!!6000000002274-2-tps-291-60.png)

聚合函数 + CASE WHEN 表达式即可实现该转换

```sql
-- CASE WHEN 实现数字列 score 行转列
SELECT name,
       SUM(CASE WHEN subject = '语文' THEN score ELSE null END) as chinese,
       SUM(CASE WHEN subject = '数学' THEN score ELSE null END) as math,
       SUM(CASE WHEN subject = '外语' THEN score ELSE null END) as english
  FROM score
 GROUP BY name;
+------+---------+------+---------+
| name | chinese | math | english |
+------+---------+------+---------+
| 张三 |      93 |   88 |      91 |
| 李四 |      87 |   90 |      77 |
+------+---------+------+---------+

-- CASE WHEN 实现文本列 subject 行转列
SELECT name,
       MAX(CASE WHEN subject = '语文' THEN subject ELSE null END) as chinese,
       MAX(CASE WHEN subject = '数学' THEN subject ELSE null END) as math,
       MIN(CASE WHEN subject = '外语' THEN subject ELSE null END) as english
  FROM score
 GROUP BY name;
+------+---------+------+---------+
| name | chinese | math | english |
+------+---------+------+---------+
| 张三 | 语文    | 数学 | 外语    |
| 李四 | 语文    | 数学 | 外语    |
+------+---------+------+---------+
```

#### 练习题

按照销售单价（ sale_price）对练习 6.1 中的 product（商品）表中的商品进行如下分类。

- 低档商品：销售单价在1000日元以下（T恤衫、办公用品、叉子、擦菜板、 圆珠笔）
- 中档商品：销售单价在1001日元以上3000日元以下（菜刀）
- 高档商品：销售单价在3001日元以上（运动T恤、高压锅）

请编写出统计上述商品种类中所包含的商品数量的 SELECT 语句。

```sql
mysql> SELECT SUM(CASE WHEN sale_price <= 1000 THEN 1 ELSE 0 END) AS
    -> low_price,
    ->  SUM(CASE WHEN sale_price BETWEEN 1001 AND 3000 THEN 1 ELSE 0 END) AS
    -> mid_price,
    ->  SUM(CASE WHEN sale_price >= 3001 THEN 1 ELSE 0 END) AS
    -> high_price
    ->  FROM product;
+-----------+-----------+------------+
| low_price | mid_price | high_price |
+-----------+-----------+------------+
|         4 |         1 |          3 |
+-----------+-----------+------------+
```

------

## Task04：集合运算 - 表的加减法和join等

### 4.1 表的加减法

#### 4.1.1 什么是集合运算

![å¾ç](https://img.alicdn.com/imgextra/i4/O1CN01xPY2gv1XHKSEPPrqr_!!6000000002898-2-tps-500-375.png)

![å¾ç](https://img.alicdn.com/imgextra/i1/O1CN016axpJu1zsi1SvV0eZ_!!6000000006770-2-tps-1156-951.png)

#### 4.1.2 表的加法 - UNION

##### 4.1.2.1 UNION

```sql
mysql> SELECT product_id, product_name
    -> FROM product
    -> UNION
    -> SELECT product_id, product_name
    -> FROM product2;
+------------+--------------+
| product_id | product_name |
+------------+--------------+
| 0001       | T恤衫        |
| 0002       | 打孔器       |
| 0003       | 运动T恤      |
| 0004       | 菜刀         |
| 0005       | 高压锅       |
| 0006       | 叉子         |
| 0007       | 擦菜板       |
| 0008       | 圆珠笔       |
| 0009       | 手套         |
| 0010       | 水壶         |
+------------+--------------+
```

**UNION 等集合运算符通常都会除去重复的记录**

对于同一张表, 实际上也是可以进行求并集的

##### 4.1.2.2 UNION 与 OR 谓词

对于同一个表的两个不同的筛选结果集, 使用 UNION 对两个结果集取并集, 和把两个子查询的筛选条件用 OR 谓词连接, 会得到相同的结果, 但倘若要将两个不同的表中的结果合并在一起, 就不得不使用 UNION 了.

而且, 即便是对于同一张表, 有时也会出于查询效率方面的因素来使用 UNION.

##### 4.1.2.3 包含重复行的集合运算 UNION ALL

SQL 语句的 UNION 会对两个查询的结果集进行合并和去重, 这种去重不仅会去掉两个结果集相互重复的, 还会去掉一个结果集中的重复行. 但在实践中有时候需要需要不去重的并集, 在 UNION 的结果中保留重复行的语法其实非常简单,只需要在 UNION 后面添加 ALL 关键字就可以了。

```mysql
-- 保留重复行
SELECT product_id, product_name
  FROM product
 UNION ALL
SELECT product_id, product_name
  FROM product2;
```

##### 4.1.2.5 隐式类型转换

有时候, 即使数据类型不完全相同, 也会通过隐式类型转换来将两个类型不同的列放在一列里显示, 例如字符串和数值类型:

#### 4.1.3 MySql 8.0 不支持交运算INTERSECT

#### 4.1.4 差集，补集与表的减法

##### 4.1.4.1 MySql 8.0 还不支持 EXCEPT 运算

MySQL 8.0 还不支持 表的减法运算符 EXCEPT. 不过, 借助第六章学过的NOT IN 谓词, 我们同样可以实现表的减法.

```mysql
-- 使用 IN 子句的实现方法
SELECT * 
  FROM product
 WHERE product_id NOT IN (SELECT product_id 
                            FROM product2)
```

使用NOT谓词进行集合的减法运算, 求出product表中, 售价高于2000,但利润低于30%的商品.

```mysql
SELECT * 
  FROM product
 WHERE sale_price > 2000 
   AND product_id NOT IN (SELECT product_id 
                            FROM product 
                           WHERE sale_price<1.3*purchase_price);
```

##### 4.1.4.4 INTERSECT 与 AND 谓词

对于同一个表的两个查询结果而言, 他们的交INTERSECT实际上可以等价地将两个查询的检索条件用AND谓词连接来实现.

```mysql
mysql> SELECT *
    -> FROM product
    -> WHERE sale_price > 1.5 * purchase_price
    -> AND sale_price < 1500;
```

#### 4.1.5 对称差

两个集合A,B的对称差是指那些仅属于A或仅属于B的元素构成的集合

两个集合的对称差等于 A-B并上B-A, 因此实践中可以用这个思路来求对称差.

### 4.2 连结

连结是 SQL 查询的核心操作

#### 4.2.1 内连结（INNER JOIN）

语法格式：

```mysql
-- 内连结
FROM <tb_1> INNER JOIN <tb_2> ON <condition(s)>
```

##### 4.2.1.1 使用内连结从两个表获取信息

```mysql
SELECT SP.shop_id
       ,SP.shop_name
       ,SP.product_id
       ,P.product_name
       ,P.product_type
       ,P.sale_price
       ,SP.quantity
  FROMshopproduct AS SP
 INNER JOIN product AS P
    ON SP.product_id = P.product_id;
```

在上述查询中, 我们分别为两张表指定了简单的别名, 这种操作在使用连结时是非常常见的, 通过别名会让我们在编写查询时少打很多字, 并且更重要的是, 会让查询语句看起来更加简洁。

**要点一: 进行连结时需要在 FROM 子句中使用多张表.**

**要点二:必须使用 ON 子句来指定连结条件.**

**要点三: SELECT 子句中的列最好按照 表名.列名 的格式来使用.**

##### 4.2.1.2 结合 WHERE 子句使用内连结

1. 第一种增加 WEHRE 子句的方式, 就是把上述查询作为子查询, 用括号封装起来, 然后在外层查询增加筛选条件.

   ```sql
   mysql> SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price, SP.quantity
       -> FROM shopproduct AS SP
       -> INNER JOIN product AS P
       -> ON SP.product_id = p.product_id
       -> WHERE SP.shop_name = '东京'
       -> AND P.product_type = '衣服';
   +---------+-----------+------------+--------------+------------+----------+
   | shop_id | shop_name | product_id | product_name | sale_price | quantity |
   +---------+-----------+------------+--------------+------------+----------+
   | 000A    | 东京      | 0001       | T恤衫        |       1000 |       30 |
   | 000A    | 东京      | 0003       | 运动T恤      |       4000 |       15 |
   +---------+-----------+------------+--------------+------------+----------+
   ```

2. 不是很常见的做法是,还可以将 WHERE 子句中的条件直接添加在 ON 子句中, 这时候 ON 子句后最好用括号将连结条件和筛选条件括起来

但上述这种把筛选条件和连结条件都放在 ON 子句的写法, 不是太容易阅读, 不建议大家使用.

```sql
mysql> SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price, SP.quantity
    -> FROM shopproduct AS SP
    -> INNER JOIN product AS P
    -> ON (SP.product_id = P.product_id AND SP.shop_name = '东京' AND P.product_type = '衣服');
```

3. 推荐写法，这种看似复杂的写法, 实际上整体的逻辑反而非常清晰. 

```sql
SELECT SP.shop_id
       ,SP.shop_name
       ,SP.product_id
       ,P.product_name
       ,P.product_type
       ,P.sale_price
       ,SP.quantity
  FROM (-- 子查询 1:从shopproduct 表筛选出东京商店的信息
        SELECT *
          FROMshopproduct
         WHERE shop_name = '东京' ) AS SP
 INNER JOIN -- 子查询 2:从 product 表筛选出衣服类商品的信息
   (SELECT *
      FROMproduct
     WHERE product_type = '衣服') AS P
    ON SP.product_id = P.product_id;
```

##### 4.2.1.3 结合 GROUP BY 子句使用内连结

每个商店中, 售价最高的商品的售价分别是多少?

```sql
SELECT SP.shop_id
      ,SP.shop_name
      ,MAX(P.sale_price) AS max_price
  FROMshopproduct AS SP
 INNER JOINproduct AS P
    ON SP.product_id = P.product_id
 GROUP BY SP.shop_id,SP.shop_name
```

##### 4.2.1.5 内连结与关联子查询

回忆第五章第三节关联子查询中的问题: 找出每个商品种类当中售价高于该类商品的平均售价的商品.当时我们是使用关联子查询来实现的.

```sql
SELECT product_type, product_name, sale_price
  FROM product AS P1
 WHERE sale_price > (SELECT AVG(sale_price)
                       FROM product AS P2
                      WHERE P1.product_type = P2.product_type
                      GROUP BY product_type);
```

**使用内连结解决：**

1. 使用 GROUP BY 按商品类别分类计算每类商品的平均价格

```sql
SELECT  product_type
       ,AVG(sale_price) AS avg_price 
  FROM product 
 GROUP BY product_type;
```

2. 将上述查询与表 product 按照 product_type (商品种类)进行内连结

```sql
SELECT  P1.product_id
       ,P1.product_name
       ,P1.product_type
       ,P1.sale_price
       ,P2.avg_price
  FROM product AS P1 
 INNER JOIN 
   (SELECT product_type,AVG(sale_price) AS avg_price 
      FROM product 
     GROUP BY product_type) AS P2 
    ON P1.product_type = P2.product_type;
```

3. 最后, 增加 WHERE 子句, 找出那些售价高于该类商品平均价格的商品.完整的代码如下:

```sql
SELECT  P1.product_id
       ,P1.product_name
       ,P1.product_type
       ,P1.sale_price
       ,P2.avg_price
  FROM product AS P1
 INNER JOIN 
   (SELECT product_type,AVG(sale_price) AS avg_price 
      FROM product 
     GROUP BY product_type) AS P2 
    ON P1.product_type = P2.product_type
 WHERE P1.sale_price > P2.avg_price;
```

##### 4.2.1.6 自然连结（NATURAL JOIN）

自然连结是内连结的一种特例 —— 当两个表进行自然连结时, 会按照两个表中都包含的列名来进行等值内连结, 此时无需使用 ON 来指定连接条件。

```sql
mysql> SELECT * FROM shopproduct
    -> NATURAL JOIN product;
+------------+---------+-----------+----------+--------------+--------------+------------+----------------+-------------+
| product_id | shop_id | shop_name | quantity | product_name | product_type | sale_price | purchase_price | regist_date |
+------------+---------+-----------+----------+--------------+--------------+------------+----------------+-------------+
| 0001       | 000A    | 东京      |       30 | T恤衫        | 衣服         |       1000 |            500 | 2009-09-20  |
| 0002       | 000A    | 东京      |       50 | 打孔器       | 办公用品     |        500 |            320 | 2009-09-11  |
| 0003       | 000A    | 东京      |       15 | 运动T恤      | 衣服         |       4000 |           2800 | NULL        |
| 0002       | 000B    | 名古屋    |       30 | 打孔器       | 办公用品     |        500 |            320 | 2009-09-11  |
| 0003       | 000B    | 名古屋    |      120 | 运动T恤      | 衣服         |       4000 |           2800 | NULL        |
| 0004       | 000B    | 名古屋    |       20 | 菜刀         | 厨房用具     |       3000 |           2800 | 2009-09-20  |
| 0006       | 000B    | 名古屋    |       10 | 叉子         | 厨房用具     |        500 |           NULL | 2009-09-20  |
| 0007       | 000B    | 名古屋    |       40 | 擦菜板       | 厨房用具     |        880 |            790 | 2008-04-28  |
| 0003       | 000C    | 大阪      |       20 | 运动T恤      | 衣服         |       4000 |           2800 | NULL        |
| 0004       | 000C    | 大阪      |       50 | 菜刀         | 厨房用具     |       3000 |           2800 | 2009-09-20  |
| 0006       | 000C    | 大阪      |       90 | 叉子         | 厨房用具     |        500 |           NULL | 2009-09-20  |
| 0007       | 000C    | 大阪      |       70 | 擦菜板       | 厨房用具     |        880 |            790 | 2008-04-28  |
| 0001       | 000D    | 福冈      |      100 | T恤衫        | 衣服         |       1000 |            500 | 2009-09-20  |
+------------+---------+-----------+----------+--------------+--------------+------------+----------------+-------------+
```

上述查询得到的结果, 会把两个表的公共列(这里是 product_id, 可以有多个公共列)放在第一列, 然后按照两个表的顺序和表中列的顺序, 将两个表中的其他列都罗列出来.

#### 4.2.2 外连结

内连结会丢去两张表中不满足ON条件的行，和内连结相对的就是外连结，外连结会根据外连结的种类有选择地保留无法匹配到的行。

外连结三种形式：

1. 左连结（保存左表中无法按照ON子句匹配到的行，对应右表的行均为缺失值）
2. 右连结（保存右表中无法按照ON子句匹配到的行，对应左表的行均为缺失值）
3. 全外连结（同时保存两个表中无法按照ON子句匹配到的行，相应的另一张表中的行用缺失值填充）

使用 LEFT 时 FROM 子句中写在左侧的表是主表,使用 RIGHT 时右侧的表是主表

```sql
-- 左连结     
FROM <tb_1> LEFT  OUTER JOIN <tb_2> ON <condition(s)>
-- 右连结     
FROM <tb_1> RIGHT OUTER JOIN <tb_2> ON <condition(s)>
-- 全外连结
FROM <tb_1> FULL  OUTER JOIN <tb_2> ON <condition(s)>
```

##### 4.2.2.2 使用左连结从两个表获取信息

```sql
mysql> SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price
    -> FROM product AS P
    -> LEFT OUTER JOIN shopproduct AS SP
    -> ON SP.product_id = P.product_id;
+---------+-----------+------------+--------------+------------+
| shop_id | shop_name | product_id | product_name | sale_price |
+---------+-----------+------------+--------------+------------+
| 000D    | 福冈      | 0001       | T恤衫        |       1000 |
| 000A    | 东京      | 0001       | T恤衫        |       1000 |
| 000B    | 名古屋    | 0002       | 打孔器       |        500 |
| 000A    | 东京      | 0002       | 打孔器       |        500 |
| 000C    | 大阪      | 0003       | 运动T恤      |       4000 |
| 000B    | 名古屋    | 0003       | 运动T恤      |       4000 |
| 000A    | 东京      | 0003       | 运动T恤      |       4000 |
| 000C    | 大阪      | 0004       | 菜刀         |       3000 |
| 000B    | 名古屋    | 0004       | 菜刀         |       3000 |
| NULL    | NULL      | NULL       | 高压锅       |       6800 |
| 000C    | 大阪      | 0006       | 叉子         |        500 |
| 000B    | 名古屋    | 0006       | 叉子         |        500 |
| 000C    | 大阪      | 0007       | 擦菜板       |        880 |
| 000B    | 名古屋    | 0007       | 擦菜板       |        880 |
| NULL    | NULL      | NULL       | 圆珠笔       |        100 |
+---------+-----------+------------+--------------+------------+
```

 MySQL8.0 目前还不支持全外连结, 不过我们可以对左连结和右连结的结果进行 UNION 来实现全外连结。

#### 4.2.3 多表连结

##### 4.2.3.1 多表进行内连结

```sql
SELECT SP.shop_id
       ,SP.shop_name
       ,SP.product_id
       ,P.product_name
       ,P.sale_price
       ,IP.inventory_quantity
  FROMshopproduct AS SP
 INNER JOINproduct AS P
    ON SP.product_id = P.product_id
 INNER JOIN Inventoryproduct AS IP
    ON SP.product_id = IP.product_id
 WHERE IP.inventory_id = 'P001';
```

##### 4.2.3.2 多表进行外连结

```sql
mysql> SELECT SP.shop_id, SP.shop_name, SP.product_id, P.product_name, P.sale_price, IP.inventory_quantity
    -> FROM product AS P
    -> LEFT OUTER JOIN shopproduct AS SP
    -> ON SP.product_id = P.product_id
    -> LEFT OUTER JOIN Inventoryproduct AS IP
    -> ON SP.product_id = IP.product_id;
```

#### 4.2.4 ON 子句进阶-非等值连结

##### 4.2.4.1 非等值自左连结（SELF JOIN）

使用非等值自左连结实现排名

```sql
SELECT  product_id
       ,product_name
       ,sale_price
       ,COUNT(p2_id) AS rank_id
  FROM (
        SELECT P1.product_id
               ,P1.product_name
               ,P1.sale_price
               ,P2.product_id AS P2_id
               ,P2.product_name AS P2_name
               ,P2.sale_price AS P2_price 
          FROM product AS P1 
          LEFT OUTER JOIN product AS P2 
            ON P1.sale_price <= P2.sale_price 
        ) AS X
 GROUP BY product_id, product_name, sale_price
 ORDER BY rank_id; 
 +------------+--------------+------------+---------+
| product_id | product_name | sale_price | rank_id |
+------------+--------------+------------+---------+
| 0005       | 高压锅       |       6800 |       1 |
| 0003       | 运动T恤      |       4000 |       2 |
| 0004       | 菜刀         |       3000 |       3 |
| 0001       | T恤衫        |       1000 |       4 |
| 0007       | 擦菜板       |        880 |       5 |
| 0002       | 打孔器       |        500 |       7 |
| 0006       | 叉子         |        500 |       7 |
| 0008       | 圆珠笔       |        100 |       8 |
+------------+--------------+------------+---------+
```

由于有两种商品的售价相同, 在使用 >= 进行连结时, 导致了累计求和错误, 这是由于这两种商品售价相同导致的. 因此实际上之前是不应该单独只用 >= 作为连结条件的. 考察我们建立自左连结的本意, 是要找出满足:1.比该商品售价更低的, 或者是 2.该种商品自身,以及 3.如果 A 和 B 两种商品售价相等,则建立连结时, 如果 P1.A 和 P2.A,P2.B 建立了连接, 则 P1.B 不再和 P2.A 建立连结, 因此根据上述约束条件, 利用 ID 的有序性, 进一步将上述查询改写为:

```sql
SELECT	product_id, product_name, sale_price
       ,SUM(P2_price) AS cum_price 
  FROM
        (SELECT  P1.product_id, P1.product_name, P1.sale_price
                ,P2.product_id AS P2_id
                ,P2.product_name AS P2_name
                ,P2.sale_price AS P2_price 
           FROM product AS P1 
           LEFT OUTER JOIN product AS P2 
             ON ((P1.sale_price > P2.sale_price)
             OR (P1.sale_price = P2.sale_price 
            AND P1.product_id<=P2.product_id))
	      ORDER BY P1.sale_price,P1.product_id) AS X
 GROUP BY product_id, product_name, sale_price
 ORDER BY sale_price,cum_price;
```

#### 4.2.5 交叉连结——CROSS JOIN （笛卡尔积）

```sql
SELECT SP.shop_id
       ,SP.shop_name
       ,SP.product_id
       ,P.product_name
       ,P.sale_price
  FROMshopproduct AS SP
 CROSS JOINproduct AS P;
```

## Task05：窗口函数等

### 5.1 窗口函数

##### 5.1.1 窗口函数概念及基本的使用方法

窗口函数也称为OLAP函数，OLAP 是OnLine AnalyticalProcessing 的简称，意思是对数据库数据进行实时分析处理。

窗口函数可以让我们有选择的去某一部分数据进行汇总、计算和排序。

```sql
<窗口函数> OVER ([PARTITION BY <列名>]
                     ORDER BY <排序用列名>)  
```

*[]中的内容可以省略。*

**PARTITON BY**是用来分组，即选择要看哪个窗口，类似于GROUP BY 子句的分组功能，但是PARTITION BY 子句并不具备GROUP BY 子句的汇总功能，并不会改变原始表中记录的行数。

**ORDER BY**是用来排序，即决定窗口内，是按那种规则(字段)来排序的。

例子：

```sql
mysql> SELECT product_name, product_type, sale_price, RANK() OVER (PARTITION BY product_type ORDER BY sale_price) AS ranking
    -> FROM product;
+--------------+--------------+------------+---------+
| product_name | product_type | sale_price | ranking |
+--------------+--------------+------------+---------+
| 圆珠笔       | 办公用品     |        100 |       1 |
| 打孔器       | 办公用品     |        500 |       2 |
| 叉子         | 厨房用具     |        500 |       1 |
| 擦菜板       | 厨房用具     |        880 |       2 |
| 菜刀         | 厨房用具     |       3000 |       3 |
| 高压锅       | 厨房用具     |       6800 |       4 |
| T恤衫        | 衣服         |       1000 |       1 |
| 运动T恤      | 衣服         |       4000 |       2 |
+--------------+--------------+------------+---------+
```

PARTITION BY 能够设定窗口对象范围。本例中，为了按照商品种类进行排序，我们指定了product_type。即一个商品种类就是一个小的"窗口"。

ORDER BY 能够指定按照哪一列、何种顺序进行排序。为了按照销售单价的升序进行排列，我们指定了sale_price。此外，窗口函数中的ORDER BY与SELECT语句末尾的ORDER BY一样，可以通过关键字ASC/DESC来指定升序/降序。

![å¾ç](https://img.alicdn.com/imgextra/i1/O1CN01zRGM7Q1QPqVqS4cVW_!!6000000001969-2-tps-862-572.png)

### 5.2 窗口函数种类

两类：

一是 将SUM、MAX、MIN等聚合函数用在窗口函数中

二是 RANK、DENSE_RANK等排序用的专用窗口函数

#### 5.2.1 专用窗口函数

- **RANK函数（英式排序）**

计算排序时，如果存在相同位次的记录，则会跳过之后的位次。

例）有 3 条记录排在第 1 位时：1 位、1 位、1 位、4 位……

- **DENSE_RANK函数（中式排序）**

同样是计算排序，即使存在相同位次的记录，也不会跳过之后的位次。

例）有 3 条记录排在第 1 位时：1 位、1 位、1 位、2 位……

- **ROW_NUMBER函数**

赋予唯一的连续位次。

例）有 3 条记录排在第 1 位时：1 位、2 位、3 位、4 位

```sql
mysql> SELECT product_name, product_type, sale_price,
    -> RANK() OVER (ORDER BY sale_price) AS ranking,
    -> DENSE_RANK() OVER (ORDER BY sale_price) AS dense_ranking,
    -> ROW_NUMBER() OVER (ORDER BY sale_price) AS row_num
    -> FROM product;
+--------------+--------------+------------+---------+---------------+---------+
| product_name | product_type | sale_price | ranking | dense_ranking | row_num |
+--------------+--------------+------------+---------+---------------+---------+
| 圆珠笔       | 办公用品     |        100 |       1 |             1 |       1 |
| 打孔器       | 办公用品     |        500 |       2 |             2 |       2 |
| 叉子         | 厨房用具     |        500 |       2 |             2 |       3 |
| 擦菜板       | 厨房用具     |        880 |       4 |             3 |       4 |
| T恤衫        | 衣服         |       1000 |       5 |             4 |       5 |
| 菜刀         | 厨房用具     |       3000 |       6 |             5 |       6 |
| 运动T恤      | 衣服         |       4000 |       7 |             6 |       7 |
| 高压锅       | 厨房用具     |       6800 |       8 |             7 |       8 |
+--------------+--------------+------------+---------+---------------+---------+
```

#### 5.2.2 聚合函数在窗口函数上的使用

```sql
mysql> SELECT product_id, product_name, sale_price,
    -> SUM(sale_price) OVER (ORDER BY product_id) AS current_sum,
    -> AVG(sale_price) OVER (ORDER BY product_id) AS current_avg
    -> FROM product;
+------------+--------------+------------+-------------+-------------+
| product_id | product_name | sale_price | current_sum | current_avg |
+------------+--------------+------------+-------------+-------------+
| 0001       | T恤衫        |       1000 |        1000 |   1000.0000 |
| 0002       | 打孔器       |        500 |        1500 |    750.0000 |
| 0003       | 运动T恤      |       4000 |        5500 |   1833.3333 |
| 0004       | 菜刀         |       3000 |        8500 |   2125.0000 |
| 0005       | 高压锅       |       6800 |       15300 |   3060.0000 |
| 0006       | 叉子         |        500 |       15800 |   2633.3333 |
| 0007       | 擦菜板       |        880 |       16680 |   2382.8571 |
| 0008       | 圆珠笔       |        100 |       16780 |   2097.5000 |
+------------+--------------+------------+-------------+-------------+
```

按我们指定的排序，这里是product_id，**当前所在行及之前所有的行**的合计或均值。即累计到当前行的聚合。

### 5.3 窗口函数的应用——计算移动平均

聚合函数在窗口函数使用时，计算的是累积到当前行的所有的数据的聚合。 实际上，还可以指定更加详细的**汇总范围**。该汇总范围成为**框架(frame)。**

```sql
<窗口函数> OVER (ORDER BY <排序用列名>
                 ROWS n PRECEDING )  
                 
<窗口函数> OVER (ORDER BY <排序用列名>
                 ROWS BETWEEN n PRECEDING AND n FOLLOWING)
```

PRECEDING（“之前”）， 将框架指定为 “截止到之前 n 行”，加上自身行

FOLLOWING（“之后”）， 将框架指定为 “截止到之后 n 行”，加上自身行

BETWEEN 1 PRECEDING AND 1 FOLLOWING，将框架指定为 “之前1行” + “之后1行” + “自身”

```sql
mysql> SELECT product_id, product_name, sale_price,
    -> AVG(sale_price) OVER (ORDER BY product_id ROWS 2 PRECEDING) AS moving_avg,
    -> AVG(sale_price) OVER (ORDER BY product_id ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING) AS moving_avg
    -> FROM product;
+------------+--------------+------------+------------+------------+
| product_id | product_name | sale_price | moving_avg | moving_avg |
+------------+--------------+------------+------------+------------+
| 0001       | T恤衫        |       1000 |  1000.0000 |   750.0000 |
| 0002       | 打孔器       |        500 |   750.0000 |  1833.3333 |
| 0003       | 运动T恤      |       4000 |  1833.3333 |  2500.0000 |
| 0004       | 菜刀         |       3000 |  2500.0000 |  4600.0000 |
| 0005       | 高压锅       |       6800 |  4600.0000 |  3433.3333 |
| 0006       | 叉子         |        500 |  3433.3333 |  2726.6667 |
| 0007       | 擦菜板       |        880 |  2726.6667 |   493.3333 |
| 0008       | 圆珠笔       |        100 |   493.3333 |   490.0000 |
+------------+--------------+------------+------------+------------+
```

![å¾ç](https://img.alicdn.com/imgextra/i1/O1CN01l9qlat1JNN3u15JEj_!!6000000001016-2-tps-898-322.png)

![å¾ç](https://img.alicdn.com/imgextra/i1/O1CN01aO6L4k1IiboQy4j3c_!!6000000000927-2-tps-920-323.png)

#### 5.3.1 窗口函数适用范围和注意事项

- 原则上，窗口函数只能在SELECT子句中使用。
- 窗口函数OVER 中的ORDER BY 子句并不会影响最终结果的排序。其只是用来决定窗口函数按何种顺序计算。

### 5.4 GROUPING运算符

#### 5.4.1 ROLLUP-计算合计及小计

常规的GROUP BY 只能得到每个分类的小计，有时候还需要计算分类的合计，可以用 ROLLUP关键字。

```sql
mysql> SELECT product_type, regist_date, SUM(sale_price) AS sum_price
    -> FROM product
    -> GROUP BY product_type, regist_date WITH ROLLUP;
+--------------+-------------+-----------+
| product_type | regist_date | sum_price |
+--------------+-------------+-----------+
| 办公用品     | 2009-09-11  |       500 |
| 办公用品     | 2009-11-11  |       100 |
| 办公用品     | NULL        |       600 |
| 厨房用具     | 2008-04-28  |       880 |
| 厨房用具     | 2009-01-15  |      6800 |
| 厨房用具     | 2009-09-20  |      3500 |
| 厨房用具     | NULL        |     11180 |
| 衣服         | NULL        |      4000 |
| 衣服         | 2009-09-20  |      1000 |
| 衣服         | NULL        |      5000 |
| NULL         | NULL        |     16780 |
+--------------+-------------+-----------+
```

![å¾ç](https://img.alicdn.com/imgextra/i1/O1CN01a2wvRr20h5aecQ6Zq_!!6000000006880-2-tps-416-219.png)

