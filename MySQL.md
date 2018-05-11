mysql -uroot -p  使用root 身份登陆mysql server        

mysqladmin -uroot -p create xxx dos命令下使用mysqladmin命令创建一个数据库    
mysqladmin -uroot -p drop xxx   dos命令下使用mysqladmin命令删除一个数据库    
CREATE DATABASE xx; mysql命令下创建一个xxx 数据库    

USE 数据库名;  选择要操作的MySQL数据库，以后所有操作只针对该数据库    

SHOW DATABASES； 显示MySQL数据库管理系统的数据库列表；    

SHOW TABLES；  显示当前操作数据库的所有表 前提是使用过 USE    

SHOW COLUMNS FROM 数据表； 显示数据表的属性，属性类型，主键信息 等一些信息
- - -
><b>CREATE TABLE table_name(column_name colun_type);</b>           
>列：属性选项 表结构         
>行：每一行就是一个表数据 eg:    
		CREATE TABLE user(
			id INT NOT NULL AUTO_INCREMENT,
			name VARCHAR(100) NOT NULL,
			age INT(3) NOT NULL,
			creat_date DATE,
			signin INT(100) NOT NULL,
			PRIMARY KEY (id)
		);
>* 如果你不想字段为 NULL 可以设置字段的属性为 NOT NULL， 在操作数据库时如果输入该字段的数据为NULL ，就会报错。    
>* AUTO_INCREMENT定义列为自增的属性，一般用于主键，数值会自动加1。    
>* PRIMARY KEY关键字用于定义列为主键。 您可以使用多列来定义主键，列间以逗号分隔  
##user    
+----+-------+-----+------------+-------------+--------+    
| id | name  | age | department | create_date | signin |    
+----+-------+-----+------------+-------------+--------+    
|  1 | John  |  20 | security   | 2018-05-08  |      6 |    
|  2 | Tom   |  25 | finance    | 2018-05-08  |      5 |    
|  3 | Jerry |  30 | logistics  | 1990-07-07  |     10 |    
|  4 | Bob   |  25 | admin      | 2018-05-09  |      3 |    
+----+-------+-----+------------+-------------+--------+     
- - -
>DROP TABLE table_name;  删除表    
- - -
><b>INSERT INTO table_name ( field1, field2,...fieldN )
                       VALUES
                       ( value1, value2,...valueN );</b> 向表中添加行数据，插入动作     	
>>* 如果数据是字符型，必须使用单引号或者双引号    
>>eg：INSERT INTO user VALUES(1,"John",20,‘1000-01-01’); 
- - -
><b>SELECT column_name,column_name FROM table_name [WHERE condition1 [AND [OR]] condition2] [OFFSET M] [LIMIT N]</b>
>>* 查询语句中你可以使用一个或者多个表，表之间使用逗号(,)分割，并使用WHERE语句来设定查询条件。
>>* SELECT 命令可以读取一条或者多条记录。
>>* 你可以使用星号（\*）来代替其他字段，SELECT语句会返回表的所有字段数据
>>* 你可以使用 WHERE 语句来包含任何条件。
>>* 你可以通过OFFSET指定SELECT语句开始查询的数据偏移量。默认情况下偏移量为0。
>>* 你可以使用 LIMIT 属性来设定返回的记录数。
>>eg: SELECT name,age FROM user WHERE name="Tom";    查找name值为Tom的数据返回由 name，age两个列组成的表，
- - -
SHOW TABLE STATUS  FROM W3CSCHOOL;   # 显示数据库 W3CSCHOOL 中所有表的信息    
SHOW TABLE STATUS from W3CSCHOOL LIKE 'W3Cschool%';     # 表名以W3Cschool开头的表的信息    
SHOW TABLE STATUS from W3CSCHOOL LIKE 'W3Cschool%'\G;   # 加上 \G，查询结果按列打印    
- - -
><b>UPDATE table_name SET field1=new_value1,field2=new_value2 [WHERE Clause];</b>
>>* 可以同时更新一个或多个字段。
>>* 可以在 WHERE 子句中指定任何条件。
>>* 可以在一个单独表中同时更新数据。
>>eg: UPDATE user SET age=40 WHERE id=1;
- - -
><b>DELETE FROM table_name [WHERE Clause];</b>
>>* 如果没有指定 WHERE 子句，MySQL表中的所有记录将被删除。
>>* 可以在 WHERE 子句中指定任何条件
>>* 可以在单个表中一次性删除记录。
>>eg: DELETE FROM user WHERE id=2;
- - -
><b>SELECT field1, field2,...fieldN 
FROM table_name1, table_name2...
WHERE field1 LIKE condition1 [AND [OR]] filed2 = 'somevalue';</b>
>>* 可以在WHERE子句中指定任何条件。
>>* 可以在WHERE子句中使用LIKE子句。
>>* 使用LIKE子句代替等号(=)。
>>* LIKE 通常与 % 一同使用，类似于一个元字符的搜索(类似 java 中 \*)。
>>* 可以使用AND或者OR指定一个或多个条件。
>>* 可以在 DELETE 或 UPDATE 命令中使用 WHERE...LIKE 子句来指定条件。
>>eg: SELECT * FROM user WHERE name LIKE '%om';
- - -
><b>ORDER BY</b>子句将查询数据排序后返回    
><b>SELECT field1,field2,...fieldN FROM table_name,table_name1... ORDER BY field1,[field2...] [ASC [DESC]];</b>    
>>* 可以使用任何字段来作为排序的条件，从而返回排序后的查询结果。    
>>* 可以设定多个字段来排序。    
>>* 可以使用 ASC 或 DESC 关键字来设置查询结果是按升序或降序排列。 默认情况下，它是按升排列。    
>>* 可以添加 WHERE...LIKE 子句来设置条件。    
>>eg:SELECT * FROM user ORDER BY name ASC; 将user表中的数据结果按name的asci码顺序排列返回    
- - -
><b>GROUP BY</b>
><b>SELECT column_name, function(column_name) FROM table_name WHERE column_name operator value GROUP BY column_name;</b>
>>eg: SELECT age, COUNT(\*) FROM user GROUP BY age;// 统计各年龄出现的次数      
 +-----+----------+    
 | age | COUNT(\*) |    
 +-----+----------+    
 |  20 |	 1 |    
 |  25 |         2 |    
 |  30 |	 1 |    
 +-----+----------+    
>><b>SELECT age, SUM(column_name) as new_column_name FROM user GROUP BY age WITH ROLLUP;</b> // 在按年龄统计基础上，再次统计column_name出现的次数和（此次展示列field = new_column_name)
>>eg: SELECT age,SUM(signin) AS signinsum FROM user GROUP BY age WITH ROLLUP;    
+-----+-----------+    
| age | signinsum |    
+-----+-----------+    
|  20 |         6 |    
|  25 |         8 |    
|  30 |        10 |    
| NULL |        24 |    
+-----+-----------+    
>>eg:SELECT coalesce(name, '总数'), SUM(singin) as singin_count FROM  employee_tbl GROUP BY name WITH ROLLUP;
>>coalesce(a,b,c);如果a==null,则选择b；如果b==null,则选择c；如果a!=null,则选择a；如果a b c 都为null ，则返回为null（没意义）。        
+------------------------+-----------+    
| coalesce(age,'allAge') | signinsum |    
+------------------------+-----------+    
| 20                     |         6 |    
| 25                     |         8 |    
| 30                     |        10 |    
| allAge                 |        24 |    
+------------------------+-----------+    
- - -
><b>MySQL连接使用</b>
>##department   
+----+------------+----------------+   
| id | department | func           |    
+----+------------+----------------+    
|  1 | security   | protect        |    
|  2 | finance    | finance stream |    
|  3 | logisitics | employ         |    
|  4 | admin      | boss           |    
+----+------------+----------------+    
>JOIN 按照功能大致分为如下三类：
>* [[INNER] JOIN]（内连接,或等值连接）：获取两个表中字段匹配关系的记录。
>* LEFT JOIN（左连接）：获取左表所有记录，即使右表没有对应匹配的记录(返回NULL)。
>* RIGHT JOIN（右连接）： 与 LEFT JOIN 相反，用于获取右表所有记录，即使左表没有对应匹配的记录（用NULL填充）。
>>eg:SELECT a.id,a.name,a.department,b.func FROM user a JOIN chair b ON a.department=b.department;    
+----+------+------------+----------------+    
| id | name | department | func           |    
+----+------+------------+----------------+    
|  1 | John | security   | protect        |    
|  2 | Tom  | finance    | finance stream |    
|  4 | Bob  | admin      | boss           |    
+----+------+------------+----------------+    
>>eg:SELECT a.id,a.name,a.department,b.func FROM user a LEFT JOIN chair b ON a.department=b.department;        
+----+-------+------------+----------------+    
| id | name  | department | func           |    
+----+-------+------------+----------------+    
|  1 | John  | security   | protect        |    
|  2 | Tom   | finance    | finance stream |    
|  4 | Bob   | admin      | boss           |    
|  3 | Jerry | logistics  | NULL           |    
+----+-------+------------+----------------+    
>>eg:SELECT a.id,a.name,a.department,b.func FROM user a RIGHT JOIN chair b ON a.department=b.department;    
+------+------+------------+----------------+    
| id   | name | department | func           |    
+------+------+------------+----------------+    
|    1 | John | security   | protect        |    
|    2 | Tom  | finance    | finance stream |    
|    4 | Bob  | admin      | boss           |    
| NULL | NULL | NULL       | employ         |    
+------+------+------------+----------------+    
- - -
><b>MySQL中的NULL：</b>    
>* IS NULL: 当列的值是NULL,此运算符返回true。    
>* IS NOT NULL: 当列的值不为NULL, 运算符返回true。    
>* <=>: 比较操作符（不同于=运算符），当比较的的两个值为NULL时返回true。    
>* MySQL中，NULL值与任何其它值的比较（即使是NULL）永远返回false.    
- - -
>MySQL中的 REGEXP
>SELECT name FROM user WHERE name REGEXP '^t'; //模糊匹配，不区分大小写；类似于
>SELECT name FROM user WHERE name LIKE "t%";
- - -
><b>MySQL ALTER</b>    
>ALTER TABLE table_name DROP field;//删除字段        
>ALTER TABLE table_name ADD field type [FIRST [AFTER field]];//增加字段        
>ALTER TABLE table_name MODIFY field type;//修改字段类型        
>ALTER TABLE table_name CHANGE field newfied[field] type;//修改字段类型及名称    
>ALTER TABLE table_name ALTER field SET DEFAULT value; //修改字段默认值        
>AlTER TABLE table_name RENAME TO new_table_name;    
- - -
数据类型：
<table>
	<tr> <th width="10%"> <strong>类型 </strong></th> <th width="15%"> <strong>大小 </strong></th> <th width="30%"> <strong>范围（有符号） </strong></th> <th width="30%"> <strong>范围（无符号） </strong></th> <th width="15%"> <strong>用途 </strong></th> </tr>
	<tr> <td> TINYINT </td> <td> 1 字节 </td> <td> (-128，127) </td> <td> (0，255) </td> <td> 小整数值 </td> </tr> 
	<tr> <td> SMALLINT </td> <td> 2 字节 </td> <td> (-32 768，32 767) </td> <td> (0，65 535) </td> <td> 大整数值 </td> </tr> 
	<tr> <td> MEDIUMINT </td> <td> 3 字节 </td> <td> (-8 388 608，8 388 607) </td> <td> (0，16 777 215) </td> <td> 大整数值 </td> </tr> 
	<tr> <td> INT或INTEGER </td> <td> 4 字节 </td> <td> (-2 147 483 648，2 147 483 647) </td> <td> (0，4 294 967 295) </td> <td> 大整数值 </td> </tr> 
	<tr> <td> BIGINT </td> <td> 8 字节 </td> <td> (-9 233 372 036 854 775 808，9 223 372 036 854 775 807) </td> <td> (0，18 446 744 073 709 551 615) </td> <td> 极大整数值 </td> </tr>
	<tr> <td> FLOAT </td> <td> 4 字节 </td> <td> (-3.402 823 466 E+38，1.175 494 351 E-38)，0，(1.175 494 351 E-38，3.402 823 466 351 E+38) </td> <td> 0，(1.175 494 351 E-38，3.402 823 466 E+38) </td> <td> 单精度<br>浮点数值 </td> </tr>
	<tr> <td> DOUBLE </td> <td> 8 字节 </td> <td> (1.797 693 134 862 315 7 E+308，2.225 073 858 507 201 4 E-308)，0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) </td> <td> 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) </td> <td> 双精度<br>浮点数值 </td> </tr> 
	<tr> <td> DECIMAL </td> <td> 对DECIMAL(M,D) ，如果M&gt;D，为M+2否则为D+2 </td> <td> 依赖于M和D的值 </td> <td> 依赖于M和D的值 </td> <td> 小数值 </td> </tr>
</table>


日期和时间类型：
<table> 
 <tr> <th width="10%"> 类型 </th> <th width="10%"> 大小<br>(字节) </th> <th width="40%"> 范围 </th> <th> 格式 </th> <th> 用途 </th> </tr>
  <tr> <td width="10%"> DATE </td> <td width="10%"> 3 </td> <td width="40%"> 1000-01-01/9999-12-31 </td> <td> YYYY-MM-DD </td> <td> 日期值 </td> </tr> 
  <tr> <td width="10%"> TIME </td> <td width="10%"> 3 </td> <td width="40%"> '-838:59:59'/'838:59:59' </td> <td> HH:MM:SS </td> <td> 时间值或持续时间 </td> </tr> 
  <tr> <td width="10%"> YEAR </td> <td width="10%"> 1 </td> <td width="40%"> 1901/2155 </td> <td> YYYY </td> <td> 年份值 </td> </tr>
  <tr> <td width="10%"> DATETIME </td> <td width="10%"> 8 </td> <td width="40%"> 1000-01-01 00:00:00/9999-12-31 23:59:59 </td> <td> YYYY-MM-DD HH:MM:SS </td> <td> 混合日期和时间值 </td> </tr>
  <tr> <td width="10%"> TIMESTAMP </td> <td width="10%"> 8 </td> <td width="40%"> 1970-01-01 00:00:00/2037 年某时 </td> <td> YYYYMMDD HHMMSS </td> <td> 混合日期和时间值，时间戳 </td> </tr>
</table>


字符串类型：
<table> 
	<tr> <th width="20%"> 类型 </th> <th width="25%"> 大小 </th> <th width="55%"> 用途 </th> </tr> 
	<tr> <td> CHAR </td> <td> 0-255字节 </td> <td> 定长字符串 </td> </tr> 
	<tr> <td> VARCHAR </td> <td> 0-65535 字节 </td> <td> 变长字符串 </td> </tr> 
	<tr> <td> TINYBLOB </td> <td> 0-255字节 </td> <td> 不超过 255 个字符的二进制字符串 </td> </tr> 
	<tr> <td> TINYTEXT </td> <td> 0-255字节 </td> <td> 短文本字符串 </td> </tr> 
	<tr> <td> BLOB </td> <td> 0-65 535字节 </td> <td> 二进制形式的长文本数据 </td> </tr> 
	<tr> <td> TEXT </td> <td> 0-65 535字节 </td> <td> 长文本数据 </td> </tr> 
	<tr> <td> MEDIUMBLOB </td> <td> 0-16 777 215字节 </td> <td> 二进制形式的中等长度文本数据 </td> </tr> 
	<tr> <td> MEDIUMTEXT </td> <td> 0-16 777 215字节 </td> <td> 中等长度文本数据 </td> </tr> 
	<tr> <td> LOGNGBLOB </td> <td> 0-4 294 967 295字节 </td> <td> 二进制形式的极大文本数据 </td> </tr> 
	<tr> <td> LONGTEXT </td> <td> 0-4 294 967 295字节 </td> <td> 极大文本数据 </td> </tr> 
</table>
	
