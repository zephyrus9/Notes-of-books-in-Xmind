## 第一部分 SQL简介 ##

SQL，指结构化查询语言，全称是 Structured Query Language。

SQL 是一种 ANSI（American National Standards Institute 美国国家标准化组织）标准的计算机语言。

RDBMS 指关系型数据库管理系统，全称 Relational Database Management System。

RDBMS 是 SQL 的基础，同样也是所有现代数据库系统的基础，比如 MS SQL Server、IBM DB2、Oracle、MySQL 以及 Microsoft Access。

## SQL 语法 ##

SHOW DATABASES;
列出 MySQL 数据库管理系统的数据库列表。


	mysql> show databases;
	+--------------------+
	| Database           |
	+--------------------+
	| information_schema |
	| mysql              |
	| performance_schema |
	| sys                |
	+--------------------+
	4 rows in set (0.03 sec)

**SQL 对大小写不敏感：SELECT 与 select 是相同的。**

### 一些最重要的 SQL 命令 ###

- SELECT：从数据库中提取数据
- UPDATE：更新数据库中的数据
- DELETE：从数据库中删除数据
- INSERT INTO：向数据库中插入新数据
- CREATE DATABASE：创建新数据库
- ALTER DATABASE：修改数据库
- CREATE TABLE：创建新表
- ALTER TABLE：变更（改变）数据库表
- DROP TABLE： 删除表
- CREATE INDEX：创建索引（搜索键）
- DROP INDEX：删除索引

## SQL SELECT 语句 ##
用于从数据库中选取数据。


## SQL SELECT DISTINCT 语句 ##
DISTINCT 关键词用于返回唯一不同的值。

## SQL WHERE 子句 ##
WHERE 子句用于过滤记录。

	SELECT * FROM Websites WHERE country='CN';
	SELECT * FROM Websites WHERE id=1;


## SQL AND & OR 运算符 ##

AND 运算符实例

	SELECT * FROM Websites
	WHERE country='CN'
	AND alexa > 50;

OR 运算符实例

	SELECT * FROM Websites
	WHERE country='USA'
	OR country='CN';

结合 AND & OR

	SELECT * FROM Websites
	WHERE alexa > 15
	AND (country='CN' OR country='USA');

## SQL ORDER BY 关键字 ##

ORDER BY 关键字用于对结果集进行排序。

### SQL ORDER BY 语法 ###

	SELECT column_name,column_name
	FROM table_name
	ORDER BY column_name,column_name ASC|DESC;
### ORDER BY 多列 ###
按照 "country" 和 "alexa" 列排序：

	SELECT * FROM Websites
	ORDER BY country,alexa;

## SQL INSERT INTO 语句 ##

INSERT INTO 实例

	INSERT INTO Websites (name, url, alexa, country)
	VALUES ('百度','https://www.baidu.com/','4','CN');

## SQL UPDATE 语句 ##

用于更新表中的记录。

SQL UPDATE 语法

	UPDATE table_name
	SET column1=value1,column2=value2,...
	WHERE some_column=some_value;

### 演示数据库 ###

		+----+--------------+---------------------------+-------+---------+
		| id | name         | url                       | alexa | country |
		+----+--------------+---------------------------+-------+---------+
		| 1  | Google       | https://www.google.cm/    | 1     | USA     |
		| 2  | 淘宝         | https://www.taobao.com/   | 13    | CN      |
		| 3  | 菜鸟教程      | http://www.runoob.com/    | 4689  | CN      |
		| 4  | 微博         | http://weibo.com/         | 20    | CN      |
		| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
		+----+--------------+---------------------------+-------+---------+
假设我们要把 "菜鸟教程" 的 alexa 排名更新为 5000，country 改为 USA。

	UPDATE websites
	SET alexa='5000', country='USA'
	WHERE name = 'Google';

**Update 警告！**

在更新记录时要格外小心！在上面的实例中，如果我们省略了 WHERE 子句，如下所示：

	UPDATE Websites
	SET alexa='5000', country='USA'
执行以上代码会将 Websites 表中所有数据的 alexa 改为 5000，country 改为 USA。

## SQL DELETE 语句 ##

DELETE 语句用于删除表中的记录。

	DELETE FROM table_name
	WHERE some_column=some_value;
	
SQL关于删除的三个语句，DROP;TRUNCATE;DELETE的区别。

- DROP:
	
	    DROP test;

删除表test，并释放空间，将test删除的一干二净。


- TRUNCATE:

		TRUNCATE test;

删除表test里的内容，并释放空间，但不删除表的定义，表的结构还在。


- DELETE:

1、删除指定数据

删除表test中年龄等于30的且国家为US的数据

	DELETE FROM test WHERE age=30 AND country='US';

2、删除整个表

仅删除表test内的所有内容，保留表的定义，不释放空间。

	DELETE FROM test 或者 DELETE FROM test;
	DELETE * FROM test 或者 DELETE * FROM test;

# 第二部分 SQL 高级教程 #
## SQL SELECT TOP, LIMIT, ROWNUM 子句 ##

### SQL SELECT TOP 子句 ###
SELECT TOP 子句用于规定要返回的记录的数目。

注意:并非所有的数据库系统都支持 SELECT TOP 语句。 MySQL 支持 LIMIT 语句来选取指定的条数数据， Oracle 可以使用 ROWNUM 来选取。

MySQL 语法

	SELECT column_name(s)
	FROM table_name
	LIMIT number;



## SQL LIKE 操作符 ##
LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。

下面的 SQL 语句选取 name 以字母 "G" 开始的所有客户：

实例
	
	SELECT * FROM Websites
	WHERE name LIKE 'G%';

## SQL 通配符 ##
在 SQL 中，通配符与 SQL LIKE 操作符一起使用。

- %：替代 0 个或多个字符
- _：替代一个字符
- [charlist]：字符列中的任何单一字符
- [^charlist]或[!charlist]：不在字符列中的任何单一字符

实例

	SELECT * FROM Websites
	WHERE url LIKE 'https%';
<img src="http://www.runoob.com/wp-content/uploads/2013/09/wildcards1.jpg">

## SQL IN 操作符 ##
IN 操作符允许您在 WHERE 子句中规定多个值。
SQL IN 语法

	SELECT column_name(s)
	FROM table_name
	WHERE column_name IN (value1,value2,...);

实例
	
	
	SELECT * FROM Websites
	WHERE name IN ('Google','菜鸟教程');
## SQL BETWEEN 操作符 ##
BETWEEN 操作符用于选取介于两个值之间的数据范围内的值。
SQL BETWEEN 语法

	SELECT column_name(s)
	FROM table_name
	WHERE column_name BETWEEN value1 AND value2;

### NOT BETWEEN 操作符实例 ###

如需显示不在上面实例范围内的网站，请使用 NOT BETWEEN：

## SQL 别名 ##
通过使用 SQL，可以为表名称或列名称指定别名。

列的 SQL 别名语法

	SELECT column_name AS alias_name
	FROM table_name;

表的 SQL 别名语法

	SELECT column_name(s)
	FROM table_name AS alias_name;

## SQL 连接(JOIN) ##

SQL JOIN 子句用于把来自两个或多个表的行结合起来，基于这些表之间的共同字段。

最常见的 JOIN 类型：SQL INNER JOIN（简单的 JOIN）。 SQL INNER JOIN 从多个表中返回满足 JOIN 条件的所有行。

### 不同的 SQL JOIN ###

- INNER JOIN：如果表中有至少一个匹配，则返回行
- LEFT JOIN：即使右表中没有匹配，也从左表返回所有的行
- RIGHT JOIN：即使左表中没有匹配，也从右表返回所有的行
- FULL JOIN：只要其中一个表中存在匹配，则返回行


<img src="http://www.runoob.com/wp-content/uploads/2013/09/img_innerjoin.gif"></img>
<img src="http://www.runoob.com/wp-content/uploads/2013/09/img_leftjoin.gif"></img>
<img src="http://www.runoob.com/wp-content/uploads/2013/09/img_rightjoin.gif"></img>
<img src="http://www.runoob.com/wp-content/uploads/2013/09/img_fulljoin.gif"></img>


## SQL UNION 操作符 ##
SQL UNION 操作符合并两个或多个 SELECT 语句的结果。

实例

	SELECT country FROM Websites
	UNION
	SELECT country FROM apps
	ORDER BY country;
### SQL UNION ALL 实例 ###

## INSERT INTO SELECT 语句 ##
INSERT INTO SELECT 语句从一个表复制数据，然后把数据插入到一个已存在的表中。

SQL INSERT INTO SELECT 语法
我们可以从一个表中复制所有的列插入到另一个已存在的表中：

	INSERT INTO table2
	SELECT * FROM table1;

实例

	INSERT INTO Websites (name, country)
	SELECT app_name, country FROM apps;

## CREATE DATABASE 语句 ##
创建数据库

## CREATE TABLE 语句 ##
创建数据库中的表。

	CREATE TABLE table_name
	(
	column_name1 data_type(size),
	column_name2 data_type(size),
	column_name3 data_type(size),
	....
	);

实例
	
	CREATE TABLE Persons
	(
	PersonID int,
	LastName varchar(255),
	FirstName varchar(255),
	Address varchar(255),
	City varchar(255)
	);

## SQL 约束 ##

- NOT NULL： 指示某列不能存储 NULL 值。
- UNIQUE： 保证某列的每行必须有唯一的值。
- PRIMARY KEY： NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。
- FOREIGN KEY： 保证一个表中的数据匹配另一个表中的值的参照完整性。
- CHECK： 保证列中的值符合指定的条件。
- DEFAULT： 规定没有给列赋值时的默认值。

MySQL：
	
	CREATE TABLE Persons
	(
	P_Id int NOT NULL,
	LastName varchar(255) NOT NULL,
	FirstName varchar(255),
	Address varchar(255),
	City varchar(255),
	PRIMARY KEY (P_Id)
	)

下面的 SQL 在 "Orders" 表创建时在 "P_Id" 列上创建 FOREIGN KEY 约束：

MySQL：

	CREATE TABLE Orders
	(
	O_Id int NOT NULL,
	OrderNo int NOT NULL,
	P_Id int,
	PRIMARY KEY (O_Id),
	FOREIGN KEY (P_Id) REFERENCES Persons(P_Id)
	)




## DROP ##
DROP 语句，可以轻松地删除索引、表和数据库。

	DROP TABLE table_name
	
	DROP DATABASE database_name
如果我们仅仅需要删除表内的数据，但并不删除表本身，

使用 TRUNCATE TABLE 语句：

	TRUNCATE TABLE table_name
## ALTER TABLE 语句 ##

ALTER TABLE 语句用于在已有的表中添加、删除或修改列。

SQL ALTER TABLE 语法
如需在表中添加列，请使用下面的语法:

	ALTER TABLE table_name
	ADD column_name datatype
如需删除表中的列，请使用下面的语法（请注意，某些数据库系统不允许这种在数据库表中删除列的方式）：
	
	ALTER TABLE table_name
	DROP COLUMN column_name

## AUTO INCREMENT 字段 ##
Auto-increment 会在新记录插入表中时生成一个唯一的数字。

下面的 SQL 语句把 "Persons" 表中的 "ID" 列定义为 auto-increment 主键字段：

	CREATE TABLE Persons
	(
	ID int NOT NULL AUTO_INCREMENT,
	LastName varchar(255) NOT NULL,
	FirstName varchar(255),
	Address varchar(255),
	City varchar(255),
	PRIMARY KEY (ID)
	)

## SQL 视图（Views） ##
视图是可视化的表。

## SQL Date 函数 ##



# SQL 函数 #
SQL 拥有很多可用于计数和计算的内建函数。


















