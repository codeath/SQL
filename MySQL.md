mysql -uroot -p  使用root 身份登陆mysql server        

mysqladmin -uroot -p create xxx dos命令下使用mysqladmin命令创建一个数据库    
mysqladmin -uroot -p drop xxx   dos命令下使用mysqladmin命令删除一个数据库    
CREATE DATABASE xx; mysql命令下创建一个xxx 数据库    

USE 数据库名;  选择要操作的MySQL数据库，以后所有操作只针对该数据库    

SHOW DATABASES； 显示MySQL数据库管理系统的数据库列表；    

SHOW TABLES；  显示当前操作数据库的所有表 前提是使用过 USE    

SHOW COLUMNS FROM 数据表； 显示数据表的属性，属性类型，主键信息 等一些信息

创建表  CREATE TABLE user(username varchar(15), userpwd varchar(15), userno int(18));     
列：属性选项 表结构         
行：每一行就是一个表数据     

向表中添加行数据，插入动作  INSERT INTO user VALUES('John', 20, 411522199709003232);    


SHOW TABLE STATUS  FROM W3CSCHOOL;   # 显示数据库 W3CSCHOOL 中所有表的信息    
SHOW TABLE STATUS from W3CSCHOOL LIKE 'W3Cschool%';     # 表名以W3Cschool开头的表的信息    
SHOW TABLE STATUS from W3CSCHOOL LIKE 'W3Cschool%'\G;   # 加上 \G，查询结果按列打印    

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
	
