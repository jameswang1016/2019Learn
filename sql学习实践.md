难点:
join与where的混合用法：
作用是从表A中a.ro_id等于表B中的b.ro_id以及 b.vx_id在[id1,id2,id3...]这个列表里面的情况下选出a.*, b.*
sql = "select a.*, b.* from %s as a join %s as b on a.ro_id = b.ro_id where b.vx_id in [id1,id2,id3...]" % (TB_A, TB_B)


	"website"表:
	+----+--------------+---------------------------+-------+---------+
	| id | name         | url                       | alexa | country |
	+----+--------------+---------------------------+-------+---------+
	| 1  | Google       | https://www.google.cm/    | 1     | USA     |
	| 2  | 淘宝          | https://www.taobao.com/   | 13    | CN      |
	| 3  | 菜鸟教程      | http://www.runoob.com/    | 4689  | CN      |
	| 4  | 微博          | http://weibo.com/         | 20    | CN      |
	| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
	+----+--------------+---------------------------+-------+---------+

- **select语句**:用于从数据库中选取数据。结果被存储在一个结果表中，称为结果集。
语法为:从 "Websites" 表中选取特定列：SELECT column_name,column_name FROM table_name;
       从 "Websites" 表中选取所有列：SELECT * FROM table_name;
  上面的含义是从%s表中 选取a.*, b.*

   select a.*, b.* from:  a.*,b.* 意思是查询A表和B表两个表的全部字段


- **select distinct**:用于返回唯一不同的值.
语法:SELECT DISTINCT column_name,column_name FROM table_name;


- **where语句**:用于提取那些满足指定标准的记录

   语法:SELECT column_name,column_name FROM table_name
       WHERE column_name operator value;
实例:下面的 SQL 语句从 "Websites" 表中选取国家为 "CN" 的所有网站：
     SELECT * FROM Websites WHERE country='CN';
      

- **and以及or**:AND & OR 运算符用于基于一个以上的条件对记录进行过滤。
  如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。

  如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。

- **order by**:ORDER BY 关键字用于对结果集进行排序
  ORDER BY 关键字用于对结果集按照一个列或者多个列进行排序。
  ORDER BY 关键字默认按照升序对记录进行排序。如果需要按照降序对记录进行排序，您可以使用 DESC 关键字(加在最后面)。
 语法:
    SELECT column_name,column_name FROM table_name
    ORDER BY column_name,column_name ASC|DESC;
 实例:(其中alexa是表中某一列的项)
    SELECT * FROM Websites ORDER BY alexa;

- **insert into**:INSERT INTO 语句用于向表中插入新记录。
语法:有两种形式:1.第一种形式无需指定要插入数据的列名，只需提供被插入的值即可：
INSERT INTO table_name VALUES (value1,value2,value3,...);
2.第二种形式需要指定列名及被插入的值：
INSERT INTO table_name (column1,column2,column3,...) VALUES (value1,value2,value3,...);

实例:INSERT INTO Websites (name, url, country) VALUES ('stackoverflow', 'http://stackoverflow.com/', 'IND');
上面的语句达到的效果:在Websites表中插入一个新行，只在 "name"、"url" 和 "country" 列插入数据（id 字段会自动更新）
**注意**在更新记录时要格外小心！在上面的实例中，如果我们省略了 WHERE 子句，如下所示：

UPDATE Websites
SET alexa='5000', country='USA'
执行以上代码会将 Websites 表中所有数据的 alexa 改为 5000，country 改为 USA。

执行没有 WHERE 子句的 UPDATE 要慎重，再慎重。

- **update**:UPDATE 语句用于更新表中已存在的记录。
 语法:UPDATE table_name SET column1=value1,column2=value2,...WHERE some_column=some_value;(WHERE 子句规定哪条记录或者哪些记录需要更新。如果您省略了 WHERE 子句，所有的记录都将被更新！)

实例:UPDATE Websites SET alexa='5000', country='USA' WHERE name='菜鸟教程';


- **delete**:DELETE 语句用于删除表中的行。

语法:DELETE FROM table_name WHERE some_column=some_value;(请注意
WHERE 子句规定哪条记录或者哪些记录需要删除。如果您省略了 WHERE 子句，所有的记录都将被删除！)

实例:DELETE FROM Websites WHERE name='百度' AND country='CN';

删除所有数据:DELETE FROM table_name;或DELETE * FROM table_name;


# SQL高级教程

- **join**:
如果有两张表Websites.id以及access_log且"Websites" 表中的 "id" 列指向 "access_log" 表中的字段 "site_id"。上面这两个表是通过 "site_id" 列联系起来的。
SELECT Websites.id, Websites.name, access_log.count, access_log.date
FROM Websites
INNER JOIN access_log
ON Websites.id=access_log.site_id;
上面语句的意思是:选取Websites表中Websites.id与access.log表中access_log.site_id相等的数据


- **create table**:
CREATE TABLE 语句用于创建数据库中的表。表由行和列组成，每个表都必须有个表名.
语法:    CREATE TABLE table_name
        (
	column_name1 data_type(size),
	column_name2 data_type(size),
	column_name3 data_type(size),
	....
	);

实例:现在我们想要创建一个名为 "Persons" 的表，包含五列：PersonID、LastName、FirstName、Address 和 City。
我们使用下面的 CREATE TABLE 语句：
CREATE TABLE Persons
(
PersonID int,
LastName varchar(255),
FirstName varchar(255),
Address varchar(255),
City varchar(255)
);
说明:PersonID 列的数据类型是 int，包含整数。    
LastName、FirstName、Address 和 City 列的数据类型是 varchar，包含字符，且这些字段的最大长度为 255 个字符。

- **NOT NULL约束**:

NOT NULL 约束强制列不接受 NULL 值。

NOT NULL 约束强制字段始终包含值。这意味着，如果不向字段添加值，就无法插入新记录或者更新记录。

语法:下面的 SQL 强制 "P_Id" 列和 "LastName" 列不接受 NULL 值：
CREATE TABLE Persons
(
P_Id int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255)
)

- **alter table**

ALTER TABLE 语句用于在已有的表中添加、删除或修改列。

语法:(1)如需在表中添加列，请使用下面的语法:ALTER TABLE table_name ADD column_name datatype
     (2)如需删除表中的列，请使用下面的语法（请注意，某些数据库系统不允许这种在数据库表中删除列的方式）：ALTER TABLE table_name DROP COLUMN column_name
     (3)要改变表中列的数据类型，请使用下面的语法：
     ALTER TABLE table_name MODIFY COLUMN column_name datatype

alter table实例:"person表如下"
P_Id	LastName	FirstName	Address	City
1	Hansen	Ola	Timoteivn 10	Sandnes
2	Svendson	Tove	Borgvn 23	Sandnes
3	Pettersen	Kari	Storgt 20	Stavanger

现在，我们想在 "Persons" 表中添加一个名为 "DateOfBirth" 的列。

我们使用下面的 SQL 语句：
ALTER TABLE Persons ADD DateOfBirth date
请注意，新列 "DateOfBirth" 的类型是 date，可以存放日期。数据类型规定列中可以存放的数据的类型。
添加列后表变成了:
P_Id	LastName	FirstName	Address	City	DateOfBirth
1	Hansen	         Ola	                Timoteivn 10	Sandnes	
2	Svendson	Tove	         Borgvn 23	Sandnes	
3	Pettersen	Kari	         Storgt 20	Stavanger	


改变数据类型实例:现在，我们想要改变 "Persons" 表中 "DateOfBirth" 列的数据类型。

ALTER TABLE Persons
ALTER COLUMN DateOfBirth year


- **SQL JOIN**

SQL join 用于把来自两个或多个表的行结合起来

SQL JOIN 子句用于把来自两个或多个表的行结合起来，基于这些表之间的共同字段。
最常见的 JOIN 类型：SQL INNER JOIN（简单的 JOIN）。 SQL INNER JOIN 从多个表中返回满足 JOIN 条件的所有行


两张表:

	+----+--------------+---------------------------+-------+---------+
	| id | name         | url                       | alexa | country |
	+----+--------------+---------------------------+-------+---------+
	| 1  | Google       | https://www.google.cm/    | 1     | USA     |
	| 2  | 淘宝          | https://www.taobao.com/   | 13    | CN      |
	| 3  | 菜鸟教程      | http://www.runoob.com/    | 4689  | CN      |
	| 4  | 微博          | http://weibo.com/         | 20    | CN      |
	| 5  | Facebook     | https://www.facebook.com/ | 3     | USA     |
	| 7  | stackoverflow | http://stackoverflow.com/ |   0 | IND     |
	+----+---------------+---------------------------+-------+---------+


	mysql> SELECT * FROM access_log;
	+-----+---------+-------+------------+
	| aid | site_id | count | date       |
	+-----+---------+-------+------------+
	|   1 |       1 |    45 | 2016-05-10 |
	|   2 |       3 |   100 | 2016-05-13 |
	|   3 |       1 |   230 | 2016-05-14 |
	|   4 |       2 |    10 | 2016-05-14 |
	|   5 |       5 |   205 | 2016-05-14 |
	|   6 |       4 |    13 | 2016-05-15 |
	|   7 |       3 |   220 | 2016-05-15 |
	|   8 |       5 |   545 | 2016-05-16 |
	|   9 |       3 |   201 | 2016-05-17 |
	+-----+---------+-------+------------+
	9 rows in set (0.00 sec)

实例:SELECT Websites.id, Websites.name, access_log.count, access_log.date
FROM Websites
INNER JOIN access_log
ON Websites.id=access_log.site_id;

结果:
https://www.runoob.com/wp-content/uploads/2013/09/join1.jpg


- **inner join**
同join:INNER JOIN 关键字在表中存在至少一个匹配时返回行。

- **left join**

SQL LEFT JOIN 关键字
LEFT JOIN 关键字**从左表（table1）返回所有的行，**(即使右表（table2）中没有匹配。如果右表中没有匹配，则结果为 NULL。

SQL LEFT JOIN 语法
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name=table2.column_name;
或：

SELECT column_name(s)
FROM table1
LEFT OUTER JOIN table2
ON table1.column_name=table2.column_name;
注释：在某些数据库中，LEFT JOIN 称为 LEFT OUTER JOIN。

SQL LEFT JOIN


- **right join**

SQL RIGHT JOIN 关键字
RIGHT JOIN 关键字从右表（table2）返回所有的行，即使左表（table1）中没有匹配。如果左表中没有匹配，则结果为 NULL。

SQL RIGHT JOIN 语法
SELECT column_name(s)
FROM table1
RIGHT JOIN table2
ON table1.column_name=table2.column_name;
或：

SELECT column_name(s)
FROM table1
RIGHT OUTER JOIN table2
ON table1.column_name=table2.column_name;
注释：在某些数据库中，RIGHT JOIN 称为 RIGHT OUTER JOIN。

SQL RIGHT JOIN
