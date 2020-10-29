# SQL语法



## 数据库表

一个数据库通常包含一个或多个表。每个表由一个名字标识（例如“客户”或者“订单”）。表包含带有数据的记录（行）。

下面的例子是一个名为 "Persons" 的表：

| ID   | LastName | FirstName | Address        | City     |
| ---- | -------- | --------- | -------------- | -------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

上面的表包含三条记录（每一条对应一个人）和五个列（Id、姓、名、地址和城市）。



## SQL语句

```Sql
SELECT LastName FROM Persons
```

结果集类似这样：

| LastName |
| :------- |
| Adams    |
| Bush     |
| Carter   |

### 重要事宜

一定要记住，**SQL 对大小写不敏感**！

### SQL语句后面的分号？

某些数据库系统要求在每条 SQL 命令的末端使用分号。在我们的教程中不使用分号。

分号是在数据库系统中分隔每条 SQL 语句的标准方法，这样就可以在对服务器的相同请求中执行一条以上的语句。

如果您使用的是 MS Access 和 SQL Server 2000，则不必在每条 SQL 语句之后使用分号，不过某些数据库软件要求必须使用分号。

### SQL DML 和 DDL

可以把 SQL 分为两个部分：数据操作语言 (DML) 和 数据定义语言 (DDL)。

SQL (结构化查询语言)是用于执行查询的语法。但是 SQL 语言也包含用于更新、插入和删除记录的语法。

查询和更新指令构成了 SQL 的 DML 部分：

- *SELECT* - 从数据库表中获取数据
- *UPDATE* - 更新数据库表中的数据
- *DELETE* - 从数据库表中删除数据
- *INSERT INTO* - 向数据库表中插入数据

SQL 的数据定义语言 (DDL) 部分使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。

SQL 中最重要的 DDL 语句:

- *CREATE DATABASE* - 创建新数据库
- *ALTER DATABASE* - 修改数据库  
- *CREATE TABLE* - 创建新表
- *ALTER TABLE* - 变更（改变）数据库表
- *DROP TABLE* - 删除表
- *CREATE INDEX* - 创建索引（搜索键）
- *DROP INDEX* - 删除索引



## SQL SELECT

SELECT 语句用于从表中选取数据。

结果被存储在一个结果表中（称为结果集）。

### SQL SELECT 语法

```
SELECT 列名称 FROM 表名称
```

以及：

```
SELECT * FROM 表名称
```

**注释：**SQL 语句对大小写不敏感。SELECT 等效于 select。

### SQL SELECT 实例

如需获取名为 "LastName" 和 "FirstName" 的列的内容（从名为 "Persons" 的数据库表），请使用类似这样的 SELECT 语句：

```
SELECT LastName,FirstName FROM Persons
```



## SQL DISTINCT

### SQL SELECT DISTINCT 语句

在表中，可能会包含重复值。这并不成问题，不过，有时您也许希望仅仅列出不同（distinct）的值。

关键词 DISTINCT 用于返回唯一不同的值。

### 语法：

```
SELECT DISTINCT 列名称 FROM 表名称
```

### 使用 DISTINCT 关键词

如果要从 "Company" 列中选取所有的值，我们需要使用 SELECT 语句：

```
SELECT Company FROM Orders
```

"Orders"表：

| Company  | OrderNumber |
| :------- | :---------- |
| IBM      | 3532        |
| W3School | 2356        |
| Apple    | 4698        |
| W3School | 6953        |

结果：

| Company  |
| :------- |
| IBM      |
| W3School |
| Apple    |
| W3School |

请注意，在结果集中，W3School 被列出了两次。

如需从 Company" 列中仅选取唯一不同的值，我们需要使用 SELECT DISTINCT 语句：

```
SELECT DISTINCT Company FROM Orders 
```

结果：

| Company  |
| :------- |
| IBM      |
| W3School |
| Apple    |

现在，在结果集中，"W3School" 仅被列出了一次。



## SQL WHERE 子句

**WHERE 子句用于规定选择的标准。**

### WHERE 子句

如需有条件地从表中选取数据，可将 WHERE 子句添加到 SELECT 语句。

语法

``````
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值
``````

下面的运算符可在 WHERE 子句中使用：

| 操作符  | 描述         |
| :------ | :----------- |
| =       | 等于         |
| <>      | 不等于       |
| >       | 大于         |
| <       | 小于         |
| >=      | 大于等于     |
| <=      | 小于等于     |
| BETWEEN | 在某个范围内 |
| LIKE    | 搜索某种模式 |

**注释：**在某些版本的 SQL 中，操作符 <> 可以写为 !=。

### 使用WHERE 子句

如果只希望选取居住在城市 "Beijing" 中的人，我们需要向 SELECT 语句添加 WHERE 子句：

``````sql
SELECT * FROM Persons WHERE City='Beijing'
``````

"Persons" 表

| LastName | FirstName | Address        | City     | Year |
| :------- | :-------- | :------------- | :------- | :--- |
| Adams    | John      | Oxford Street  | London   | 1970 |
| Bush     | George    | Fifth Avenue   | New York | 1975 |
| Carter   | Thomas    | Changan Street | Beijing  | 1980 |
| Gates    | Bill      | Xuanwumen 10   | Beijing  | 1985 |

结果：

| LastName | FirstName | Address        | City    | Year |
| :------- | :-------- | :------------- | :------ | :--- |
| Carter   | Thomas    | Changan Street | Beijing | 1980 |
| Gates    | Bill      | Xuanwumen 10   | Beijing | 1985 |

### 引号的使用

请注意，我们在例子中的条件值周围使用的是单引号。

SQL 使用单引号来环绕*文本值*（大部分数据库系统也接受双引号）。如果是*数值*，请不要使用引号。

文本值：

```sql
这是正确的：
SELECT * FROM Persons WHERE FirstName='Bush'

这是错误的：
SELECT * FROM Persons WHERE FirstName=Bush
```

数值：

```sql
这是正确的：
SELECT * FROM Persons WHERE Year>1965

这是错误的：
SELECT * FROM Persons WHERE Year>'1965'
```



## SQL AND & OR 运算符

**AND 和 OR 运算符用于基于一个以上的条件对记录进行过滤。**

### AND 和 OR 运算符

AND 和 OR 可在 WHERE 子语句中把两个或多个条件结合起来。

如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。

如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。

### 原始的表 (用在例子中的)：

| LastName | FirstName | Address        | City     |
| :------- | :-------- | :------------- | :------- |
| Adams    | John      | Oxford Street  | London   |
| Bush     | George    | Fifth Avenue   | New York |
| Carter   | Thomas    | Changan Street | Beijing  |
| Carter   | William   | Xuanwumen 10   | Beijing  |

### AND 运算符实例

使用 AND 来显示所有姓为 "Carter" 并且名为 "Thomas" 的人：

```
SELECT * FROM Persons WHERE FirstName='Thomas' AND LastName='Carter'
```

结果：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Carter   | Thomas    | Changan Street | Beijing |

### OR 运算符实例

使用 OR 来显示所有姓为 "Carter" 或者名为 "Thomas" 的人：

```
SELECT * FROM Persons WHERE firstname='Thomas' OR lastname='Carter'
```

结果：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Carter   | Thomas    | Changan Street | Beijing |
| Carter   | William   | Xuanwumen 10   | Beijing |

### 结合 AND 和 OR 运算符

我们也可以把 AND 和 OR 结合起来（使用圆括号来组成复杂的表达式）:

```sql
SELECT * FROM Persons WHERE (FirstName='Thomas' OR FirstName='William')
AND LastName='Carter'
```

结果：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Carter   | Thomas    | Changan Street | Beijing |
| Carter   | William   | Xuanwumen 10   | Beijing |



## SQL ORDER BY 子句

**ORDER BY 语句用于对结果集进行排序。**

### ORDER BY 语句

ORDER BY 语句用于根据指定的列对结果集进行排序。

ORDER BY 语句默认按照升序对记录进行排序。

如果您希望按照降序对记录进行排序，可以使用 DESC 关键字。

### 原始的表 (用在例子中的)：

Orders 表:

| Company  | OrderNumber |
| :------- | :---------- |
| IBM      | 3532        |
| W3School | 2356        |
| Apple    | 4698        |
| W3School | 6953        |

### 实例 1

以字母顺序显示公司名称：

```
SELECT Company, OrderNumber FROM Orders ORDER BY Company
```

结果：

| Company  | OrderNumber |
| :------- | :---------- |
| Apple    | 4698        |
| IBM      | 3532        |
| W3School | 6953        |
| W3School | 2356        |

### 实例 2

以字母顺序显示公司名称（Company），并以数字顺序显示顺序号（OrderNumber）：

```
SELECT Company, OrderNumber FROM Orders ORDER BY Company, OrderNumber
```

结果：

| Company  | OrderNumber |
| :------- | :---------- |
| Apple    | 4698        |
| IBM      | 3532        |
| W3School | 2356        |
| W3School | 6953        |

### 实例 3

以逆字母顺序显示公司名称：

```
SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC
```

结果：

| Company  | OrderNumber |
| :------- | :---------- |
| W3School | 6953        |
| W3School | 2356        |
| IBM      | 3532        |
| Apple    | 4698        |

### 实例 4

以逆字母顺序显示公司名称，并以数字顺序显示顺序号：

```
SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC, OrderNumber ASC
```

结果：

| Company  | OrderNumber |
| :------- | :---------- |
| W3School | 2356        |
| W3School | 6953        |
| IBM      | 3532        |
| Apple    | 4698        |

**注意：**在以上的结果中有两个相等的公司名称 (W3School)。只有这一次，在第一列中有相同的值时，第二列是以升序排列的。如果第一列中有些值为 nulls 时，情况也是这样的。

## SQL INSERT INTO 语句

INSERT INTO 语句用于向表格中插入新的行。

### 语法

```
INSERT INTO 表名称 VALUES (值1, 值2,....)
```

我们也可以指定所要插入数据的列：

```
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)
```

### 插入新的行

"Persons" 表：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Carter   | Thomas    | Changan Street | Beijing |

SQL 语句：

```sql
INSERT INTO Persons VALUES ('Gates', 'Bill', 'Xuanwumen 10', 'Beijing')
```

结果：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Carter   | Thomas    | Changan Street | Beijing |
| Gates    | Bill      | Xuanwumen 10   | Beijing |

### 在指定的列中插入数据

"Persons" 表：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Carter   | Thomas    | Changan Street | Beijing |
| Gates    | Bill      | Xuanwumen 10   | Beijing |

SQL 语句：

```sql
INSERT INTO Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')
```

结果：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Carter   | Thomas    | Changan Street | Beijing |
| Gates    | Bill      | Xuanwumen 10   | Beijing |
| Wilson   |           | Champs-Elysees |         |



## SQL UPDATE 语句

Update 语句用于修改表中的数据。

### 语法：

```sql
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
```

Person：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Gates    | Bill      | Xuanwumen 10   | Beijing |
| Wilson   |           | Champs-Elysees |         |

更新某一行中的一列

我们为 lastname 是 "Wilson" 的人添加 firstname：

```sql
UPDATE Person SET FirstName = 'Fred' WHERE LastName = 'Wilson' 
```

结果：

| LastName | FirstName | Address        | City    |
| :------- | :-------- | :------------- | :------ |
| Gates    | Bill      | Xuanwumen 10   | Beijing |
| Wilson   | Fred      | Champs-Elysees |         |

### 更新某一行中的若干列

我们会修改地址（address），并添加城市名称（city）：

```sql
UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing'
WHERE LastName = 'Wilson'
```

结果：

| LastName | FirstName | Address      | City    |
| :------- | :-------- | :----------- | :------ |
| Gates    | Bill      | Xuanwumen 10 | Beijing |
| Wilson   | Fred      | Zhongshan 23 | Nanjing |



## SQL DELETE 语句

DELETE 语句用于删除表中的行。

### 语法

```sql
DELETE FROM 表名称 WHERE 列名称 = 值
```

Person:

| LastName | FirstName | Address      | City    |
| :------- | :-------- | :----------- | :------ |
| Gates    | Bill      | Xuanwumen 10 | Beijing |
| Wilson   | Fred      | Zhongshan 23 | Nanjing |

### 删除某行

"Fred Wilson" 会被删除：

```
DELETE FROM Person WHERE LastName = 'Wilson' 
```

结果:

| LastName | FirstName | Address      | City    |
| :------- | :-------- | :----------- | :------ |
| Gates    | Bill      | Xuanwumen 10 | Beijing |

### 删除所有行

可以在不删除表的情况下删除所有的行。这意味着表的结构、属性和索引都是完整的：

```sql
DELETE FROM table_name
```

或者：

```sql
DELETE * FROM table_name
```



# 高级教程

## SQL TOP 子句

TOP 子句用于规定要返回的记录的数目。

对于拥有数千条记录的大型表来说，TOP 子句是非常有用的。

**注释：**并非所有的数据库系统都支持 TOP 子句。

### SQL Server 的语法：

```sql
SELECT TOP number|percent column_name(s)
FROM table_name
```

### MySQL 和 Oracle 中的 SQL SELECT TOP 是等价的

#### MySQL 语法

```mysql
SELECT column_name(s)
FROM table_name
LIMIT number
```

例子

```sql
SELECT *
FROM Persons
LIMIT 5
```

#### Oracle 语法

```sql
SELECT column_name(s)
FROM table_name
WHERE ROWNUM <= number
```

例子

```sql
SELECT *
FROM Persons
WHERE ROWNUM <= 5
```



原始的表 (用在例子中的)：

Persons 表:

| Id   | LastName | FirstName | Address             | City       |
| :--- | :------- | :-------- | :------------------ | :--------- |
| 1    | Adams    | John      | Oxford Street       | London     |
| 2    | Bush     | George    | Fifth Avenue        | New York   |
| 3    | Carter   | Thomas    | Changan Street      | Beijing    |
| 4    | Obama    | Barack    | Pennsylvania Avenue | Washington |

SQL TOP 实例

现在，我们希望从上面的 "Persons" 表中选取头两条记录。

我们可以使用下面的 SELECT 语句：

```
SELECT TOP 2 * FROM Persons
```

结果：

| Id   | LastName | FirstName | Address       | City     |
| :--- | :------- | :-------- | :------------ | :------- |
| 1    | Adams    | John      | Oxford Street | London   |
| 2    | Bush     | George    | Fifth Avenue  | New York |



SQL TOP PERCENT 实例

现在，我们希望从上面的 "Persons" 表中选取 50% 的记录。

我们可以使用下面的 SELECT 语句：

```
SELECT TOP 50 PERCENT * FROM Persons
```

结果：

| Id   | LastName | FirstName | Address       | City     |
| :--- | :------- | :-------- | :------------ | :------- |
| 1    | Adams    | John      | Oxford Street | London   |
| 2    | Bush     | George    | Fifth Avenue  | New York |



## SQL LINK

**LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。**

### SQL LIKE 操作符语法

```
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern
```

### 原始的表 (用在例子中的)：

Persons 表:

| Id   | LastName | FirstName | Address        | City     |
| :--- | :------- | :-------- | :------------- | :------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

### LIKE 操作符实例

例子 1

现在，我们希望从上面的 "Persons" 表中选取居住在以 "N" 开始的城市里的人：

我们可以使用下面的 SELECT 语句：

```
SELECT * FROM Persons
WHERE City LIKE 'N%'
```

**提示：**"%" 可用于定义通配符（模式中缺少的字母）。

结果集：

| Id   | LastName | FirstName | Address      | City     |
| :--- | :------- | :-------- | :----------- | :------- |
| 2    | Bush     | George    | Fifth Avenue | New York |



<hr/>

例子 2

接下来，我们希望从 "Persons" 表中选取居住在以 "g" 结尾的城市里的人：

我们可以使用下面的 SELECT 语句：

```
SELECT * FROM Persons
WHERE City LIKE '%g'
```

结果集：

| Id   | LastName | FirstName | Address        | City    |
| :--- | :------- | :-------- | :------------- | :------ |
| 3    | Carter   | Thomas    | Changan Street | Beijing |



<hr/>

例子 3

接下来，我们希望从 "Persons" 表中选取居住在包含 "lon" 的城市里的人：

我们可以使用下面的 SELECT 语句：

```
SELECT * FROM Persons
WHERE City LIKE '%lon%'
```

结果集：

| Id   | LastName | FirstName | Address       | City   |
| :--- | :------- | :-------- | :------------ | :----- |
| 1    | Adams    | John      | Oxford Street | London |





<hr/>

例子 4

通过使用 NOT 关键字，我们可以从 "Persons" 表中选取居住在*不包含* "lon" 的城市里的人：

我们可以使用下面的 SELECT 语句：

```
SELECT * FROM Persons
WHERE City NOT LIKE '%lon%'
```

结果集：

| Id   | LastName | FirstName | Address        | City     |
| :--- | :------- | :-------- | :------------- | :------- |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |