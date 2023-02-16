## MySQL 基础篇

#### 数据库概念

- 数据库
  - 存储数据的仓库，数据是有组织的进行存储
  - DataBase (DB)
- 数据库管理系统
  - 操纵和管理数据库的大型软件
  - DataBase Management System (DBMS)
- SQL
  - 操作关系型数据库的编程语言，定义了一套操作关系型数据库统一标准
  - Structured Query Language (SQL)

#### 关系型数据库 （RDBMS）

概念：

建立在关系模型基础上，由多张相互连接的二维表组成的数据库。

特点：

1. 使用表存储数据，格式统一，便于维护
2. 使用SQL语言操作，标准统一，使用方便



数据模型： 







## SQL

#### SQL 通用语法

1. SQL 语句可以单行或多行书写，以分好结尾。
2. SQL语句可以使用空格/缩进来增强语句的可读性。
3. MySQL数据库的SQL 语句不区分大小写，关键字建议使用大写。
4. 注释：
   1. 单行注释： -- 注释内容或#注释内容（MySQL特有）
   2. 多行注释： /* 注释内容*/

#### SQL 分类

- DDL 

  - Data Definition language 
  - 数据库定义语言，用来定义数据库对象（数据库，表，字段）

- DML

  - Data Manipulation language 
  - 数据库操作语言，用来对数据库表中的数据进行增删改

- DQL

  - Data Query language
  - 数据查询语言，用来查询数据库中表的记录

- DCL

  - Data Control language
  - 数据控制语言，用来创建数据库用户，控制数据库的访问权限

  

#### DDL

 - 查询

   - 查询所有数据库

     ```sql
     SHOW DATABASES;
     ```

   - 查询当前数据库

     ```sql
     SELECT DATABASE();
     ```

 - 创建

   ```sql
   CREATE DATABASE [IF NOT EXISTS]数据库名 [DEFAULT CHARSET 字符集][COLLATE 排序规则];
   ```

   

 - 删除

   ```sql
   DROP DATABASE [IF EXISTS] 数据库名;
   ```

 - 使用

   ```sql
   USE 数据库名;
   ```



#### DDL 表查询

- 查询当前数据库所有表

  ```sql
  SHOW TABLES;
  ```

- 查询表结构

  ```sql
  DESC 表名;
  ```

- 查询指定表的建表语句

  ```sql
  SHOW CREATE TABLE 表名;
  ```

#### DDL 表操作 创建

```sql
CREATE TABLE 表名 （
	字段1 字段1类型[COMMENT 字段1注释],
	字段2 字段2类型[COMMENT 字段2注释],
）[COMMENT 表注释];
```

#### DDL 表操作 数据类型

- 数值类型 

  ![截屏2023-02-12 下午1.42.27](/Users/lidongyang/Library/Application Support/typora-user-images/截屏2023-02-12 下午1.42.27.png)

- 字符串类型

  ```
  CHAR    0-255 bytes  定长字符
  VARCHAR 0-65535 bytes  变长字符串
  TINYBLOB 0-255 bytes 不超过255个字符的二进制数据
  TINYTEXT 0-255 bytes 短文本字符串
  BLOB     0-65535 bytes 二进制形式的长文本数据
  TEXT   0-65535 bytes 长文本数据
  MEDIUMBLOB  二进制形式的中等长度文本数据
  MEDIUMTEXT  中等长度文本数据
  LONGBLOB  二进制形式的极大文本数据
  LONGTEXT  极大文本数据
  ```

  ![截屏2023-02-12 下午1.45.10](/Users/lidongyang/Library/Application Support/typora-user-images/截屏2023-02-12 下午1.45.10.png)

- 日期时间类型

  ```
  DATE   1000-01-01至9999-12-31  YYYY-MM-DD 日期值
  TIME   -838:59:59至838:59:59 HH:MM:SS 时间值或持续时间
  YEAR   1901至2155            YYYY  年份值
  DATETIME  1000-01-01 00:00:00 至9999-12-31 23:59:59  YYYY-MM-DD HH:MM:SS  混合日期和时间值
  TIMESTAMP  1970-01-01 00:00:01 至2038-01-19 03:14:07  YYYY-MM-DD HH:MM:SS 混合日期和时间值 时间戳 
  ```

  ![截屏2023-02-12 下午1.46.11](/Users/lidongyang/Library/Application Support/typora-user-images/截屏2023-02-12 下午1.46.11.png)



#### DDL 表操作 修改

- 添加字段

  ```sql
  ALTER TABLE 表名 ADD 字段名 类型（长度）[COMMENT 注释][约束];
  ```

- 修改字段

  ```sql
  ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度)[COMMENT 注释][约束];
  ```

- 修改数据类型

  ```sql
  ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);
  ```

- 修改字段名和字段类型

  ```sql
  ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度)[COMMENT 注释][约束];
  ```

- 删除字段

  ```
  ALTER TABLE 表名 DROP 字段名;
  ```

- 修改表名

  ```sql
  ALTER TABLE 表名 RENAME TO 新表名;
  ```

- 删除表

  - 删除表

  ```sql
  DROP TABLE [IF EXISTS]表名;
  ```

  - 删除指定表，并重新创建该表

    ```sql
    TRUNCATE TABLE 表名;
    ```

  注意：在删除表的时候，表中的数据也会被删除。

#### DML

DML 英文全称是 Data Manipulation language（数据操作语言）用来对数据库中表的数据记录进行增删改操作。

- 添加数据（INSERT）

  - 给指定字段添加数据

  ```sql
  INSERT INTO 表名(字段名1， 字段名2， ...) VALUES (值1, 值1, ....);
  ```

  - 给全部字段添加数据

    ```sql
    INSERT INTO 表名 VALUES(值1,值2, ...);
    ```

  - 批量添加数据

    ```sql
    INSERT INTO 表名(字段1,字段2,...) VALUES(值1,值2,...),(值1,值2,...);
    ```

    ```sql
    INSERT INTO 表名 VALUES(值1,值2,...),(值1,值2,...),(值1,值2,...);
    ```

    

- 修改数据（UPDATE）

  ```sql
  UPDATE 表名 SET 字段名1=值1, 字段名2=值2, ...[WHERE 条件];
  ```

  注意：修改语句的条件可以有，也可以没有，如果没有条件，则会修改整张表的所有数据。

- 删除数据 （DELETE）

  ```sql
  DELETE FROM 表名 [WHERE 条件]
  ```

  注意：

  - DELETE语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据。
  - DELETE语句不能删除某一个字段的值(可以使用UPDATE)。

#### DQL

Data Query language（数据查询语言），数据查询语言，用来查询数据库中表的记录。

查询关键字： SELECT

```sql
SELECT 
	字段列表
FROM 
	表名列表
WHERE
	条件列表
GROUP BY
	分组字段列表
HAVING
	分组后条件列表
ORDER BY
	排序字段列表
LIMIT
	分页参数
```

- 基本查询

  - 查询多个字段

    ```sql
    SELECT 字段1,字段2,字段3... FROM 表名;
    ```

    ```sql
    SELECT * FROM 表名;
    ```

  - 设置别名

    ```sql
    SELECT 字段1[AS 别名1], 字段2[AS 别名2]... FROM 表名;
    ```

  - 去除重复记录

    ```sql
    SELECT DISTINCT 字段列表 FROM 表名;
    ```

    

- 条件查询（WHERE）

  1. 语法

     ```sql
     SELECT 字段列表 FROM 表名 WHERE 条件列表;
     ```

  2. 条件 关键字 WHERE

     1. `>` 大于
     2. `>=` 大于等于
     3. `<` 小于
     4. `<=` 小于等于
     5. `=` 等于
     6. `<> 或 !=` 不等于
     7. `BETWEEN...ADN...`  在某个范围之内(含最小, 最大值)
     8. `IN(...)` 在in之后的列表中的值，多选一
     9. `LIKE 占位符` 模糊匹配(_匹配单个字符, %匹配任意个字符)
     10. `IS NULL` 是NULL
     11. `AND 或 &&` 并且(多个条件同时成立)
     12. `OR 或||` 或者(多个条件任意一个成立)
     13. `NOT 或 ！` 非，不是

- 聚合函数（count,max,min,avg,sum）

  1. 将一列数据作为一个整体，进行纵向计算。

  2. 常见的聚合函数

     1. count (统计数量)
     2. max (最大值)
     3. min (最小值)
     4. avg (平均值)
     5. sum (求和)

  3. 语法

     ```sql
     SELECT 聚合函数（字段列表）FROM 表名;
     ```

     注意： null值不参与所有聚合函数运算

- 分组查询（GROUP BY）

  1. 语法

     ```sql
     SELECT 字段列表 FROM 表名 [WHERE 条件] GROUP BY 分组字段名 [HAVING  分组后过滤条件];
     ```

  2. Where 与having 区别

     1. 执行时机不同： where 是分组之前进行过滤，不满足where条件，不参与分组；而having 是分组之后对结果进行过滤。
     2. 判断条件不同：where不能对聚合函数进行判断, 而having可以。 

  注意：

  - 执行属性： where > 聚合函数 > having；
  - 分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义。

- 排序查询  (ORDER BY)

  1. 语法

     ```sql
     SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1，字段2 排序方式2;
     ```

  2. 排序方式

     - ASC： 升序(默认值)
     - DESC：降序

  注意： 如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序。

- 分页查询 (LIMIT)

  1. 语法

     ```sql
     SELECT 字段列表 FROM 表名 LIMIT 起始索引,查询记录数;
     ```

  注意：

  - 起始索引从0开始，起始索引 = （查询页码 - 1）* 每页显示记录数。
  - 分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT;
  - 如果查询的是第一页数据,起始索引可以省略,直接简写为limit 10。

  ```sql
  1. 查询年龄为20，21,22,23岁的女性员工信息。
  SELECT * from emp where age in(20,21,22,23) and gender = "女";
  
  2.查询性别为男，并且年龄在20-40岁(含)以内的姓名为三个字的员工。
  SELECT * from emp where gender = "男" and age between 20 and 40 and name like'_ _ _';
  
  3. 统计员工表中，年龄小于60岁的，男性员工和女性员工的人数.
  SELECT gender, count(*) from emp where age <= 60 group by gender ;
  
  4. 查询所有年龄小于等于35岁员工的姓名和年龄，并对查询结果按年龄升序排序，如果年龄相同按入职时间降序排序。
  SELECT name,age from emp where age <= 35 order by age, entrydata desc;
  
  5. 查询性别为男，且年龄在20-40岁(含)以内的前5个员工信息，对查询的结果按年龄升序排序，年龄相同按入职时间升序排序。
  SELECT * from emp where gender = '男' and between 20 and 40 order by age asc, entrydata asc limit 5 ;
  ```

  #### DQL 执行顺序
  
  - 编写顺序
  
  ```sql
  SELECT 
  	字段列表
  FROM 
  	表名列表
  WHERE
  	条件列表
  GROUP BY
  	分组字段列表
  HAVING
  	分组后条件列表
  ORDER BY
  	排序字段列表
  LIMIT
  	分页参数
  ```
  
  - 执行顺序
  
    ```sql 
    FROM 
    	表名列表
    WHERE 
    	条件列表
    GROUP BY
    	分组字段列表
    HAVING 
    	分组后条件列表
    SELECT 
    	字段列表
    ORDER BY
    	排序字段列表
    LIMIT
    	分页参数
    ```
  
    

#### DCL

 Data Control language (数据控制语言)，用来管理数据库用户，控制数据库的访问权限。

#### DCL 管理用户

1. 查询用户

   ```sql
   USE mysql;
   SELECT * FROM user;
   ```

2. 创建用户

   ```sql
   CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码'；
   ```

3. 修改用户密码

   ```sql
   ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';
   ```

4. 删除用户

   ```sql
   DROP USER '用户名'@'主机名';
   ```

   注意：

   - 主机名可以使用%通配。
   - 这类SQL开发人员操作的比较少，主要是DBA（Database Administratior 数据库管理员）使用。

#### DCL 权限控制 

MySQL中定义了很多种权限，但是常用的就是以下几种：

- ALL， ALL PRIVILEGES  所有权限
- SELECT  查询权限
- INSERT 插入数据
- UPDATE 修改数据
- DELETE 删除数据
- ALTER 修改表
- DROP 删除数据库/表/视图
- CREATE  创建数据库/表



1. 查询权限

```sql
SHOW GRANTS FOR '用户名'@'主机名';
```

2. 授予权限

```sql
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
```

3. 撤销权限

```sql
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
```



注意：

- 多个权限之间，使用逗号分隔
- 授权时，数据库名和表名可以使用*进行通配，代表所有。



## 函数

函数是指一段可以直接被另一段程序调用的程序或代码。

```sql
SELECT 函数(参数);
```



#### 字符串函数

MySQL中内置了很多字符串函数，常用的几个如下：

- CONCAT(S1,S2,S3,...Sn);     字符串拼接，将S1,S2,...Sn拼接成一个字符串。
- LOWER(str)  将字符串str全部转为小写
- UPPER(str) 将字符串str 全部转为大写
- LPAD(str,n,pad)  左填充，用字符串pad对str的左边进行填充，达到n个字符串长度。
- RPAD(str,n,pad) 右填充，用字符串pad对str的右边进行填充，达到n个字符串长度。
- TRIM(str) 去掉字符串头部和尾部的空格
- SUBSTRING(str,start,len)  返回字符串str 从start位置起的len个长度的字符串。

```sql
SELECT 函数(参数);
```



#### 数值函数

常见的数值函数如下：

- CEIL(x) 向上取整
- FLOOR(x) 向下取整
- MOD(x,y) 返回x/y的模
- RAND()返回0-1内的随机数
- ROUND(x,y) 求参数x的四舍五入的值，保留y位小数

练习：

通过数据库的函数，生成一个六位数的随机验证码

```sql
select lpad(round(rand() * 1000000, 0), 6, '0');
```



#### 日期函数

常见的日期函数：

- CURDATE()  返回当前日期
- CURTIME() 返回当前时间
- NOW()  返回当前日期和时间
- YEAR(date) 获取指定date的年份
- MONTH(date) 获取指定date的月份
- DAY(date) 获取指定date的日期
- DATE_ADD(date, INTERVAL expr type) 返回一个日期/时间值加上一个时间间隔expr后的时间值
- DATEDIFF(date1, date2) 返回起始时间date1和结束时间date2之间的天数

#### 流程函数

流程函数也是很常用的一类函数，可以在SQL语句中实现条件筛选，从而提高语句的效率。

- IF(value, t, f)  如果value为true,则返回t, 否则返回f
- IFNULL(value1, value2) 如果value1不为空，返回value1,否则返回value2
- CASE WHEN [val1] THEN [res1] ... ELSE [default] END  如果val1为true,返回res1,....否则返回default默认值
- CASE [expr] WHEN [val1] THEN [res1].... ELSE[default] END  如果expr的值等于val1，返回res1，...否则返回defalut默认值。



## 约束

1. 概念： 约束是作用于表中字段上的规则，用于限制存储在表中的数据。

2. 目的：保证数据库中数据的正确，有效性和完整性。

3. 分类：

   ```excel
   约束         描述                                    关键字
   1.非空约束     限制该字段的数据不能为null                NOT NULL
   2.唯一约束     保证该字段的所有数据都是唯一，不重复的       UNIQUE
   3.主键约束     主键是一行数据的唯一标识，要求非空且唯一      PRIMARY KEY
   4. 默认约束     保存数据时，如果未指定该字段的值，则采取默认值   DEFAULT
   5. 检查约束(8.0.16版本之后)  保证字段值满足某一个条件          CHECK
   6.外键约束       用来让两张表的数据之间建立连接，保证数据的一致性和完整性   FOREIGN KEY
   ```

   AUTO_INCREMENT 自动增长

   

#### 外键约束

概念：

外键用来让两张表的数据之间建立连接，从而保证数据的一致性和完整性。

语法

- 添加外键

  ```SQL
  CREATE TABLE 表名(
    字段 数据类型，
    ...
    [CONSTRAINT][外键名称] FOREIGN KEY (外键字段名) REFERENCES 主表(主表列名)
  );
  ```

  ```sql
  ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段名) REFERENCES 主表(主表列名);
  ```

- 删除外键

  ```sql
  ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
  ```

- 删除/更新行为

  - NO ACTION  当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。（与RESTRICT一致）
  - RESTRICT 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键,如果有则不允许删除/更新。（与NO ACTION一致）
  - CASCADE 当在父表中删除/更新对应记录时,首先检查该记录是否有对应外键,如果有,则也删除/更新外键在子表中的记录。
  - SET NULL 当在父表中删除对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为null(这就要求该外键允许取null)
  - SET DEFAULT 父表有变更时，子表将外键列设置成一个默认的值（Innodb 不支持）

  语法：

  ```sql
  ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段)REFERENCES 主表名(主表字段名) ON UPDATE CASCADE ON DELETE CASCADE;
  ```

  

## 多表查询

#### 多表关系

项目开发中，在进行数据库表结构设计时，会根据业务需求及业务模块之间的关系，分析并设计表结构，由于业务之间相互关联，所以各个表结构之间也存在着各种联系，基本分为三种：

- 一对多（多对一）

  - 案例： 部门与员工的关系

  - 关系：一个部门对应多个员工，一个员工对应一个部门

  - 实现： 在多的一方建立外键，指向一的一方的主键

    



- 多对多

  - 案例： 学生与课程的关系

  - 关系： 一个学生可以选修多门课程，一门课程也可以供多个学生选择

  - 实现：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键。

    

- 一对一

  - 案例： 用户与用户详情的关系
  - 关系： 一对一关系，多用于单表拆分，将一张表的基础字段放在一张表中，其他详情字段放在另一张表中，以提升操作效率。
  - 实现： 在任意一方加入外键，关联另外一方的主键，并且设置外键为唯一的（UNIQUE）

#### 多遍查询概述

概述： 指从多张表中查询数据

多表查询-- 笛卡尔积

笛卡尔积：笛卡尔积乘积是指在数学中，两个集合 A集合和B集合的所有组合情况。（在多表查询时，需要消除无效的笛卡尔积）

语法

```sql
SELECT * FROM 表1,表2 where 表1.关联的column = 表2.关联的column；
```



##### 多表查询分类

- 连接查询
  - 内连接： 相当于查询A，B交集部分数据
  - 外连接：
    - 左外连接： 查询左表所有数据，以及两张表交集部分数据
    - 右外连接： 查询右表所有数据，以及两张表交集部分数据
  - 自连接： 当前表与自身的连接查询，自连接必须使用表别名。
- 子查询

#### 内连接

 内连接查询的是两张表交集的部分

- 隐式内连接

  - ```sql
    SELECT 字段列表 FROM 表1,表2 WHERE 条件...;
    ```

- 显式内连接

  - ```sql
    SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 连接条件...;
    ```

#### 外连接

- 左外连接

  - 相当于查询表1（左表）的所有数据包含表1和表2交集部分的数据。

  ```sql
  SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 条件...;
  ```

- 右外连接

  - 相当于查询表2（右表）的所有数据包含表1和表2交集部分的数据。

  ```sql
  SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件...;
  ```

  

#### 自连接

自连接查询语法：

```sql
SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 条件...;
```

自连接查询，可以是内连接查询，也可以是外连接查询。



#### 联合查询 union, union all

对于union查询，就是把多次查询的结果合并起来，形成一个新的查询结果集。

```sql
SELECT 字段列表 FROM 表A ...
UNION[ALL]
SELECT 字段列表 FROM 表B...;
```

- UNION ALL 是直接将两个查询结果合并
- UNION 是将两个查询结果合并并且去重。

注意：

- 对于联合查询的多张表的列数必须保持一致，字段类型也需要保持一致。
- UNION ALL 是直接将两个查询结果合并，UNION是将两个查询结果合并并且去重。

#### 子查询

- 概念： SQL语句中嵌套SELECT语句，称为嵌套查询，又称子查询

  ```sql
  SELECT * FROM t1 WHERE column = (SELECT column1 FROM t2);
  ```

  子查询外部的语句可以是`INSERT/UPDATE/DELETE/SELECT`的任何一个。

- 根据子查询结果不同，分为

  - 标量子查询（子查询结果为单个值）
  - 列子查询（子查询结果为一列）
  - 行子查询（子查询结果为一行）
  - 表子查询（子查询结果为多行多列）

- 根据子查询位置，分为：WHERE之后、FROM之后、SELECT之后。

#### 多表查询案例

- 标量子查询

  - 子查询返回的结果是单个值（数字、字符串、日期等），最简单的形式，这种子查询成为标量子查询。

  - 常用的操作符：`= <> > >= < <=`

- 列子查询
  - 子查询返回的结果是一列（可以是多行），这种子查询成为列子查询。
  - 常用的操作符： `IN、NOT IN、ANY、SOME、ALL`
    - IN 在指定的集合范围之内，多选一
    - NOT IN 不在指定的集合范围之内
    - ANY 子查询返回列表中，有任意一个满足即可
    - SOME 与ANY 等同，使用SOME的地方都可以使用ANY
    - ALL 子查询返回列表的所有值都必须满足
