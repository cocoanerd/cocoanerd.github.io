## 1、初始MySQL
javaEE:企业级java开发 

Web:前端（页面：展示，数据！）

后台：（连接点：链接数据库JDBC，链接前端（控制，控制视图跳转，和给前端传递数据））

数据库：存取数据（Txt、Excel、word）

### 1.1、为什么要学习数据库
1、岗位需求

2、现在的世界，大数据时代~，得数据库者得天下

3、被迫需求：存数据

4、数据库是所有软件体系中最核心的存在 DBA

### 1.2、什么是数据库

数据库（DB, DataBase）

概念：数据仓库，软件，安装在操作系统（window,linux,mac、...）之上！（主要侧重SQL，操作数据库的语句），可以存储大量的数据。500万！

作用：存储数据，管理数据

### 1.3、数据库分类
关系型数据库：Excel （SQL）
- MySQL, Oracle, Sql Server, DB2, SQLlite
- 通过表和表之间，行和列之间的关系进行数据的存储，学员信息表，考勤表，...

非关系行数据库: {key: value} （NoSQL）Not Only SQL
- Redis, MongDB
- 非关系型数据库，对象存储，通过对象的自身的属性来决定

== DBMS(数据库管理系统) ==

- 数据库的管理软件,科学有效的管理我我们的数据。维护和获取数据；
- MySQL,数据库管理系统！

### 1.4、MySQL简介
MySQL 是一个关系型数据库管理系统

前世：瑞典MySQL AB公司

今生：属于Oracle旗下产品

MySQL是最好的RDBMS（Relational Database Management System,关系数据库管理系统）应用软件之一。

开源的数据库软件:体积小、速度快、成本低

适用于中小型网站、或者大型网站，集群！

官网：https://www.mysql.com


5.7稳定  


安装建议：
1、尽量不要使用exe，注册表
2、尽可能使用压缩包安装

### 1.5、安装MySQL

修改密码：

> cd /usr/local/mysql/bin/
> sudo su
> ./mysqld_safe --skip-grant-tables &
> exit
> ./mysql -u root
> show databases;
> use mysql;
>  update user set authentication_string='' where User='root';


### 1.6、链接数据库：
命令行链接！

> mysql -uroot -p --链接数据库 
>
> flush privileges; -- 刷新权限
> 
> 所有的语句都是用；结尾
>
> show databases; -- 查看所有的数据库
>
> mysql> use school -- 切换数据库 use 数据库名>
>
> Database changed>
>
> show tables; -- 查看数据库中所有的表
>
> describe student; -- 显示数据库中所有的表的信息
>
> create database westos; -- 创建一个数据库
> 
> exit; -- 退出链接
>
> 单行注释 -- (SQL本来的注释) 
>
> /* 多行注释>*/


#### 数据库xxx语言 CRUD增删改查！ CV（赋值粘贴）  API（调用各种api）  CRUD（业务程序员）
- DDL 定义
- DML 操作
- DQL 查询
- DCL 控制


## 2、操作数据库（了解）
操作数据库 > 操作数据库中的表 > 操作数据库中标的数据

-- mysql 关键字不区分带小写

### 2.1 数据库操作
- 创建数据库
> CREATE DATABASE IF NOT EXISTS westos;

- 删除数据库
> DROP	DATABASE IF EXISTS westos;


- 使用数据库
> -- table 键的上面，如果你的表名或字段名是一个特殊字符，就需要带``
> USE `school`

- 查看数据库
> SHOW DATABASE -- 查看所有数据库

### 2.2、数据库的列类型
> 数值
- tinyint 		十分小的数据 			1个字节
- smalint 		较小的数据			2个字节
- mediumint		中等大小的数据		3个字节
- int 	 		标准的整数			4个字节  常用
- big int 		较大的数据			8个字节
- float 		浮点数				4个字节
- double		浮点数				8个字节 精度问题
- decimal   	字符串形式的浮点数 金融计算的时候一般使用decimal 

> 字符串
- char 			字符串固定大小 	0-255
- varchar		可变字符串	 	0-65535		常用的变量 对应java String
- tinytext		微型文本			2^8-1
- text			文本串			2^16-1		保存大文本

> 时间日期
java.util.Date	
- date 			YYYY-MM-DD				日期格式
- time			HH:mm:ss 				时间格式
- datetime		YYYY-MM-DD HH:mm:ss 	最常用的时间格式
- timestamp 	时间戳  					1970.1.1到现在的毫秒数 较为常用
- year			年份

> null
- 没有值，未知
- 注意：不要使用NULL进行运算，结果为NULL

### 2.3、数据库的字段属性（重点）
Unsigned:
- 无符号的证书
- 声明了该列不能声明为负数

zerofill:
- 0填充
- 不足的位数，使用0来填充 10  0000000001

自增：
- 通常理解为自增，自动在上一条记录的基础上+1（默认）
- 通常用来设计唯一的主键 index, 必须是整数类型
- 可以自定义设置主键的起始值和步长

null not null:
- 假设设置为not null,如果不给他赋值就会报错！
- null, 如果不填写值，默认就是null

默认：
- 设置默认值！
- sex,默认值为男，如果不指定该列的值，则会有默认值


拓展：

```
/*
	每个表都必须存在以下五个字段！
	id 				主键
	`version`		版本
	is_delete		伪删除
	gmt_create		创建时间
	gmt_update		修改时间
*/

```

### 2.4、创建数据库表

```
-- 目标：创建学生表（列，字段） 使用SQL 创建
-- 学号int 登录密码varchar（20）姓名，性别varchar(2)，出生日期datatime, 家庭住址， email
-- 注意点：使用英文（），表的名称和字段尽量使用``括起来
-- 所有的语句后面加，（英文的最后一个不用加）
CREATE TABLE `student` (
  `id` int NOT NULL AUTO_INCREMENT COMMENT '学号',
  `name` varchar(30) NOT NULL DEFAULT '匿名' COMMENT '姓名',
  `pwd` varchar(20) NOT NULL DEFAULT '123456' COMMENT '密码',
  `sex` varchar(2) NOT NULL DEFAULT '男' COMMENT '性别',
  `birthday` datetime DEFAULT NULL COMMENT '出生日期',
  `address` varchar(100) DEFAULT '' COMMENT '家庭住址',
  `email` varchar(50) DEFAULT '' COMMENT '邮箱',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

格式

> CREATE TABLE [IF NOT EXISTS] `表名` (
>
>	`字段名` 列类型 [属性] [索引] [注释],
>
>	`字段名` 列类型 [属性] [索引] [注释],
>
>  ......
>
> 	`字段名` 列类型 [属性] [索引] [注释]
>
>)[表类型][字符集设置][注释]


### 2.5、数据库标的类型


```
-- 关于数据库引擎
/*
	INNODB 默认使用
	MYISAM 早些年使用
*/

```

| Column 1  	| MYISAM  	| INNODB  	|
|:----------	|:---------	|:----------|
| 事务支持    	| 不支持    	| 支持    	|
| 数据行锁定   	| 不支持    	| 支持    	|
| 外键约束    	| 不支持   	| 支持    	|
| 全文索引    	| 支持    	| 不支持    	|
| 表空间的大小 	| 较小    	| 较大 约为2倍    |

常规使用操作：
- MYISAM 节约空间、速度较快
- INNODB 安全性高、事务的处理、多表多用户操作

> 在物理空间存在的位置
所有的数据库文件都存在data目录下, 一个文件夹对应一个数据库

本质还是文件的存储

MySQL引擎在物理文件上的区别
- INNODB 在数据库表中只有一个*.frm文件，以及上级目录下的ibdata1文件
- MYISAM 对应的文件
 	- .frm - 表结构的定义文件
	- .MYD 数据文件（data）
	- .MYI 索引文件（index）


> 设置数据库表的字符集编码
> CHARSET-UTF8
不设置的话，回事mysql的默认字符集编码，不支持中文

在my.ini中配置默认的编码，但是不推荐，如果别人电脑没有设置
> character-set-server-utf8

### 2.6、修改删除表

> 修改
```
-- 修改表 ALTER TABLE 旧表名 RENAME AS 新表名
ALTER TABLE teacher RENAME AS teacher1
-- 增加表的字段
ALTER TABLE teacher1 ADD age INT(11)
-- 修改表的字段（重命名，修改约束）
-- ALTER TABLE 表名 MODIFY 字段名 列属性[]
ALTER TABLE teacher1 MODIFY age VARCHAR(11) -- 修改约束
-- ALTER TABLE 表名 CHANGE  旧名字 新名字 列属性[]
ALTER TABLE teacher1 CHANGE age age1 INT(11) -- 字典重命名

-- 删除表的字段 ALTER TABLE 表名 DROP 字段名
ALTER TABLE teacher1 DROP age1

```

> 删除
```
-- 删除表 如果表存在再删除
DROP TABLE IF EXISTS teacher1
```

注意点：
- `` 字段名，使用这个包裹！
- 注释 -- /**/
- sql 关键字大小写不敏感，建议大家写小写
- 所有的符号全部用英文

## 3、MySQL数据管理

### 3.1、外键（了解即可）
> 方式一：在创建表的时候，增加约束（麻烦、比较复杂）

```
CREATE TABLE IF NOT EXISTS `grade` (
	`gradeid` INT(10) NOT NULL AUTO_INCREMENT COMMENT '年级id',
	`gradename` VARCHAR(50) NOT NULL COMMENT '年级名称',
	PRIMARY KEY (`gradeid`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 注意点：使用英文（），表的名称和字段尽量使用``括起来
-- 所有的语句后面加，（英文的最后一个不用加）
-- 学生表的gradeid字段 要去引用年级表的gradeid
-- 定义外键key
-- 给这个外键添加约束（执行引用）references 引用
CREATE TABLE IF NOT EXISTS `student` (
	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
	`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名', 
	`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
	`sex` VARCHAR(2) NOT NULL DEFAULT '男' COMMENT '性别',
	`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
	`gradeid` INT(10) NOT NULL COMMENT '学生的年级',
	`address` VARCHAR(100) DEFAULT '' COMMENT '家庭住址',
	`email` VARCHAR(50) DEFAULT '' COMMENT '邮箱',
	PRIMARY KEY (`id`),
	KEY `FK_gradeid` (`gradeid`),
	CONSTRAINT `FK_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `grade` (`gradeid`)
)ENGINE=INNODB DEFAULT CHARSET=utf8
```
删除有外键关系的表的时候，必须要先删除引用别人的表（从表），再删除被引用的表（主表）
> 方式二：创建表成功后，添加外键约束 创建表的时候没有外键关系
```
CREATE TABLE IF NOT EXISTS `grade` (
	`gradeid` INT(10) NOT NULL AUTO_INCREMENT COMMENT '年级id',
	`gradename` VARCHAR(50) NOT NULL COMMENT '年级名称',
	PRIMARY KEY (`gradeid`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 目标：创建学生表（列，字段） 使用SQL 创建
-- 学号int 登录密码varchar（20）姓名，性别varchar(2)，出生日期datatime, 家庭住址， email
-- 注意点：使用英文（），表的名称和字段尽量使用``括起来
-- 所有的语句后面加，（英文的最后一个不用加）
-- 学生表的gradeid字段 要去引用年级表的gradeid
-- 定义外键key
-- 给这个外键添加约束（执行引用）references 引用
CREATE TABLE IF NOT EXISTS `student` (
	`id` INT(4) NOT NULL AUTO_INCREMENT COMMENT '学号',
	`name` VARCHAR(30) NOT NULL DEFAULT '匿名' COMMENT '姓名', 
	`pwd` VARCHAR(20) NOT NULL DEFAULT '123456' COMMENT '密码',
	`sex` VARCHAR(2) NOT NULL DEFAULT '男' COMMENT '性别',
	`birthday` DATETIME DEFAULT NULL COMMENT '出生日期',
	`gradeid` INT(10) NOT NULL COMMENT '学生的年级',
	`address` VARCHAR(100) DEFAULT '' COMMENT '家庭住址',
	`email` VARCHAR(50) DEFAULT '' COMMENT '邮箱',
	PRIMARY KEY (`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 创建表的时候没有外键关系
ALTER TABLE `student`
ADD CONSTRAINT `FK_gradeid` FOREIGN KEY (`gradeid`) REFERENCES `grade` (`gradeid`)
```

以上操作都是物理外键，数据库级别的外键，我们不建议使用！（避免数据库过多造成困扰，这里了解即可）

最佳实践
- 数据库就是单纯的表，只用来存数据，只有行（数据）和列（字段）
- 我们想使用多张表的数据，想使用外键（程序去实现）
### 3.2 DML语言（全部记住，背下来）
数据库的意义：数据存储，数据管理

DML语言：数据操作语言
- insert
- update
- delete

### 3.3 添加ss
> insert
```
-- 插入语句（添加）
-- insert into 表名（[字段名1,字段2,字段3]）values（'值1'),（'值2'),('值3', ...）
INSERT INTO `grade` (`gradename`) VALUES('大四')

-- 由于主键自增我们可以省略 （如果不写表的字段，就会一一匹配）
INSERT INTO `grade` VALUES('大三')

-- 一般写插入语句，我们一定要数据和字段一一对应
-- 插入多个字段
INSERT INTO `grade` (`gradename`) 
VALUES('大二'),('大一')

INSERT INTO `student` (`name`) VALUES ('张三')
INSERT INTO `student` (`name`,`pwd`,`sex`) VALUES ('张三','aaaa','男')
```
语法：insert into 表名（[字段名1,字段2,字段3]）values（'值1'),（'值2'),('值3', ...）
注意事项：
	1. 字段和字段之间使用英文逗号隔开
	2. 字段是可以省略的，但是后面的值必须要一一对应，不能减少
	3. 可以同时插入多条数据，value后面的值，需要使用，隔开即可VALUES(),(),(),.....

### 3.4 修改
> update 修改谁 （条件） set 原来的值 = 新值
```
-- 修改学院名字
UPDATE `student` SET `name`='狂神' WHERE id = 1;
-- 不指定条件的情况下，会改动所有表！
UPDATE `student` SET `name`='长江7号'

-- 语法：
-- UPDATE 表名 SET colnum_name = value WHERE [条件]
```

条件：where子句 运算符 id等于某个值，大于某个值，在某个区间内修改...
| 操作符  	| 含义  		| 范围  	| 结果  |
|:---------	|:----------|:----------|:----------|
| =    				| 等于    		| 5=6    | false    |
| <> 或 !=   		| 不等于    		| 5<>6   | false    |
| >, < , <= , >= 	|     			|     	 |     |
| BETWEEN... and...	| 在某个范围内   	| [2,5]  |     |
| AND    			| 我和你&&  		|  5>1 and 1>2  |  false  |
| OR    			| 我或你||    	|  5>1 or 1>2  | true    |

```
-- 通过多个条件定位数据
UPDATE `student` SET `name`='长江7号' WHERE `name`='狂神' AND `sex`='女'
```

语法：UPDATE 表名 SET colnum_name=value,[colnum_name=value,...] WHERE [条件]
注意：
- colnum_name 是数据库的列，尽量带上``
- 条件，筛选的条件，如果没有指定，则会修改所有列
- value,是一个具体的值，也可以是一个变量
- 多个设置的属性之间，使用英文逗号隔开

### 3.5 删除
> delete命令
语法：delete from 表名 [where(条件)]

```
-- 删除数据 (避免这样写,会全部删除)
DELETE FROM `student`
-- 删除指定数据
DELETE FROM `student` WHERE id = 1
```
> TRUNCATE命令
作用：完全清空一个数据库表，表的结构和索引约束不会变

```
-- 清空 student 表
TRUNCATE `student`
```
> delete 和 TRUNCATE 区别
- 相同点：都能删除数据，都不会删除表结构
- 不同：
	- TRUNCATE 重新设置 自增列 计数器会归零
	- TRUNCATE 不会影响事务
```
-- test delete he truncate区别
CREATE TABLE IF NOT EXISTS `test` (
	`id` INT(4) NOT NULL AUTO_INCREMENT,
	`coll` VARCHAR(20) NOT NULL,
	PRIMARY KEY (`id`)
)ENGINE=INNODB DEFAULT CHARSET=UTF8

INSERT INTO `test` (`coll`) VALUES('1'),('2'),('3')

DELETE FROM `test` -- 不会影响自增

TRUNCATE TABLE `test` -- 自增会归零
```
了解即可： DELETE删除的问题，重启数据库，现象
- INNODB 自增列会重1开始（存在内存当中，断电即失）
- MYISAM 继续从上一个自增量开始（存在文件中的，不会丢失）


## 4、DQL查询数据（最重点）

### 4.1、DQL
（Data Query LANGUAGE:数据查询语言）
- 所有查询操作都用它，select
- 简单的查询，复杂的查询它都能做
- 数据库中最核心的语言，最重要的语句
- 使用频率最高的语句

select完整的语法
>  SELECT语法
```
SELECT [ALL | DISTINCT]
{* | table.* | [table.field1[as alias1][,table.field2[as alias2]][,...]]}
FROM table_name [as table_alias]
	[left | right | inner join table_name2] -- 联合查询
	[WHERE ...] -- 指定结果需要满足的条件
	[GROUP BY ...] -- 指定结果按照哪几个字段来分组
	[HAVING] -- 过滤分组的记录必须满足的次要条件
	[ORDER BY ...] -- 指定查询记录按一个或多个条件排序
	[LIMIT {[offset,]row_count | row_countOFFSET offset}]; -- 指定查询的记录从哪条至哪条

```
注意：[]括号代表可选的，{}代表必选的

### 4.2、指定查询字段
```
-- 查询全部的学生 SELECT 字段 FROM 表
SELECT * FROM student

-- 查询指定字段
SELECT `StudentNo`,`StudentName` FROM student

-- 别名，给结果起一个名字 AS 也可以给字段起别名，也可以给表起别名
SELECT `StudentNo` AS 学号,`StudentName` AS 学生姓名 FROM student AS s

-- 函数 Concat(a,b)
SELECT CONCAT('姓名：', StudentName) AS 新名字 FROM student
```
语法：SELECT 字段,... FROM 表

> 有的时候，列名字不是那么见名知意。我们可以起别名 AS  字段名 as 别名  表名 as 别名


> 去重 distinct

作用：去除SELECT查询出来的结果中重复的数据，只显示一条
```
-- 查询一下有哪些同学参加了考试，成绩
SELECT * FROM result -- 查询全部的考试成绩
SELECT `studentNo` FROM result -- 查询有哪些同学参加了考试
SELECT DISTINCT `studentNo` FROM result -- 发现重复数据，去重 
```
> 数据库的列（表达式）
```
SELECT VERSION() -- 查看系统版本（函数）
SELECT 100*3-1 AS 计算结果 -- 用来计算（表达式）
SELECT @@auto_increment_increment -- 查询自增的步长（变量）

-- 学员考试成绩+1分查看
SELECT `StudentNo`,`StudentResult`+1 AS '提分后' FROM result
```
数据库中的表达式：文本值，列，Null，函数，计算表达式，系统变量......

select 表达式 from 表

### 4.3、where条件子句
作用：检索数据中`符合条件`的值

搜索的条件由一个或多个表达式组成！结果都是一个布尔值
> 逻辑运算符
| 运算符 | 语法  | 描述  |
|:----------|:----------|:----------|
| and  &&  	|  	a and b  a&&b   |  逻辑与，两个都为真，结果为真  |
| or  ||  	| 	a or b  a||b    	| 逻辑或，其中一个为真，则结果为真   |
| Not !   	|  	not a  !a 		 | 逻辑非 ，真为假，假为真  |

尽量使用英文字母
```
-- =====================where=========================
SELECT studentNo, `StudentResult` FROM result

-- 查询考试成绩在95到100分之间的
SELECT studentNo, `StudentResult` FROM result
WHERE StudentResult>=95 AND StudentResult<=100

-- and &&
SELECT studentNo, `StudentResult` FROM result
WHERE StudentResult>=95 && StudentResult<=100

-- 模糊查询（区间）
SELECT studentNo, `StudentResult` FROM result
WHERE StudentResult BETWEEN 95 AND 100


-- 除了1000号学生之外的同学的成绩
SELECT studentNo, `StudentResult` FROM result
WHERE studentNo NOT 1000

-- != not
SELECT studentNo, `StudentResult` FROM result
WHERE studentNo!=1000
```


> 模糊查询：比较运算符

| 运算符 | 语法  | 描述  |
|:----------|:----------|:----------|
| IS NULL  	|  	a is null   |  如果操作符为null，则结果为真  |
| IS NOT NULL  	| 	a is not null    	| 如果操作符不为null，则结果为真   |
| BETWEEN   	|  	a between b and c 		 | 若a在b和c之间，则结果为真  |
| LIKE			| 	a like b			| SQL匹配，如果a匹配b，则结果为真
| IN			|	a in (a1,a2,a3,...) | 假设a在a1,或者a1,...其中的某个一值，结果为真


```
-- =====================模糊查询=========================
-- 查询姓刘的同学
-- like结合 %(代表0到任意个字符) _(一个字符)
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '刘%'

-- 查询姓刘的同学，名字后面只有一个字的
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '刘_'

-- 查询姓刘的同学，名字后面只有两个字的
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '刘__'

-- 查询名字当中有嘉字的同学
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentName LIKE '%嘉%'

-- ====================== in（具体的一个或者多个值） ========================
-- 查询1001，1002，1003号的学员
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE StudentNo IN (1001,1002,1003)

-- 查询在北京的学生
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE `Address` IN ('北京','河南洛阳')

-- ====================== null   not null ========================
-- 查询地址为空的同学 null ''
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE address = '' OR ADDRESS IS NULL

-- 查询有出生日期的同学 不为空
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE BornDate IS NOT NULL

-- 查询没有出生日期的同学 
SELECT `StudentNo`,`StudentName` FROM `student`
WHERE BornDate IS NULL
```

### 4.4、联表查询
> JOIN 对比
![avatar](https://img-blog.csdnimg.cn/20181103160140252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h1YW5nX18y,size_16,color_FFFFFF,t_70)


| 操作  | 描述  |
|:----------|:----------|
| inner join | 如果表中至少有一个匹配，就返回行   |
| left join  |  会从左表中返回所有的值，即使右表中没有匹配   |
| right join | 会从右表中返回所有的值，即使左表中没有匹配    |

```
-- ====================== 联表查询 join ========================
-- 查询参加了考试的同学（学号，姓名，科目编号，分数）
SELECT * FROM student
SELECT * FROM result

/* 思路
1.分析需求，分析查询的字段来自哪些表，（连接查询）
2.确定使用哪种连接查询？7种
确定交叉点（这两个表中，哪个数据是相同的）
判断的条件：学生表中的studentNo = 成绩表 studentNo=成绩表 studentNo
*/

-- join on 连接查询 
-- where   等值查询
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student AS s
INNER JOIN result AS r
WHERE s.studentNo = r.studentNo

-- Right join  AS 可以省略
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student s
RIGHT JOIN result r
ON s.studentNo = r.studentNo

-- Left join 
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student s
LEFT JOIN result r
ON s.studentNo = r.studentNo

-- 查询缺考的同学
SELECT s.studentNo,studentName,SubjectNo,StudentResult
FROM student s
LEFT JOIN result r
ON s.studentNo = r.studentNo
WHERE StudentResult IS NULL

-- 思考题（查询了参加考试的同学信息：学号，学生姓名，科目名称，分数）
/* 思路
1.分析需求，分析查询的字段来自哪些表，student、result 、 subject（连接查询）
2.确定使用哪种连接查询？7种
确定交叉点（这两个表中，哪个数据是相同的）
判断的条件：学生表中的studentNo = 成绩表 studentNo=成绩表 studentNo
*/
SELECT s.studentNo,studentName,SubjectName,StudentResult
FROM student s
RIGHT JOIN result r
ON r.studentNo = s.studentNo
INNER JOIN `subject` sub
ON r.SubjectNo = sub.SubjectNo

-- 我要查询哪些数据select...
-- 从哪几个表中查 FROM 表 xxx join 连接的表  on 交叉条件 
-- 假设存在一种多张表查询，慢慢来，先查询两张表，然后再慢慢增加


-- From a left join b  以a表为基准
-- From a right join b  以b表为基准
```

> 自连接(了解)
自己的表和自己的表连接，核心：**一张表拆为两张一样的表即可**

父类

| categoryid | categoryName |
|:----------|:----------|
| 2   |  信息技术 |
| 3   |  软件开发 |
| 5   |  美术设计 |


子类

|pid  | categoryid | categoryName |
|:---------|:----------|:----------|
| 3   |  4 |  数据库 |
| 2   |  8 |  办公信息 |
| 3   |  6 |  web开发 |
| 5   |  7 |  美术设计 |

操作：查询父类对应的子类关系

| 父类 | 子类 |
|:----------|:----------|
| 信息技术   |  办公信息 |
| 软件开发   |  数据库 |
| 软件开发   |  web开发 |
| 美术设计   |  ps技术 |



### 4.5、分页和排序

> 排序
```
-- ==================== 分页(limit)和排序(order by) =====================
-- 排序：升序 ASC ，降序 DESC
-- ORDER BY 通过哪个字段排序，怎么排
-- 查询的记过根据成绩排序
SELECT `StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
FROM student s
INNER JOIN `result` r
ON s.`StudentNo` = r.`StudentNo`
INNER JOIN `subject` sub 
ON r.`SubjectNo` = sub.`SubjectNo`
WHERE subjectName = '数据库结构-1'
ORDER BY StudentResult DESC
```

> 分页
```
-- 分页 每页只显示5条数据
-- LIMIT 起始值，页面的大小
-- 网页应用：当前，总的页数，页的大小
-- LIMIT 0,5 1~5
-- LIMIT 1,5 2~6
-- LIMIT 6,5 5~10
SELECT `StudentNo`,`StudentName`,`SubjectName`,`StudentResult`
FROM student s
INNER JOIN `result` r
ON s.`StudentNo` = r.`StudentNo`
INNER JOIN `subject` sub 
ON r.`SubjectNo` = sub.`SubjectNo`
WHERE subjectName = '数据库结构-1'
ORDER BY StudentResult DESC
LIMIT 0,5

-- 第一页 limit 0,5   		(1-1)*5
-- 第二页 limit 6,5			(2-1)*5
-- 第三页 limit 10,5			(3-1)*5
-- 第N页 limit ,5				(n-1)*pageSize, pageSize
-- pageSize：页面大小  
-- (n-1)*pageSize：起始值
-- n代表当前页
-- 总数：数据总数/页面大小
```

语法：limit(起始值，pageSize)


### 4.6 子查询
where(这个值是计算出来的)

本质：在where语句中嵌套一个子查询语句

where (select * form)
```

-- ==================== where =====================
-- 1、查询数据库结构-1 的所有考试结果（学号，科目编号，成绩），降序排列
-- 方式一：使用连接查询
SELECT `StudentNo`, r.`SubjectNo`, `StudentResult`
FROM `result` r 
INNER JOIN `subject` sub
ON r.SubjectNo = sub.SubjectNo
WHERE SubjectName = '数据库结构-1'
ORDER BY StudentResult DESC

-- 方式二：使用子查询（由里及外）
SELECT `StudentNo`, `SubjectNo`, `StudentResult`
FROM `result`
WHERE SubjectNo = (
	-- 查询所有数据库机构-1的学生的学号
	SELECT SubjectNo FROM `subject` 
	WHERE SubjectName = '数据库结构-1'
)
ORDER BY StudentResult DESC

-- 查询课程为高等数学-2 且 分数不小于80分的同学的学号和姓名
SELECT s.StudentNo, StudentName
FROM student 
INNER JOIN result r
ON s.StudentNo = r.StudentNo
INNER JOIN `subject` sub
ON r.`SubjectNo` = sub.`SubjectNo`
WHERE `SubjectName` = '高等数学-2' AND `StudentResult` >= 80

-- 分数不小于80分的学生的学号和姓名
SELECT DISTINCT `StudentNo`, `StudentName`
FROM `student` s 
INNER JOIN result r
ON s.StudentNo = r.StudentNo
WHERE `StudentResult` >= 80

-- 在这个基础上增加一个科目，高等数学-2 
-- 查询高等数学-2的编号
SELECT DISTINCT `StudentNo`, `StudentName`
FROM `student` s 
INNER JOIN result r
ON s.StudentNo = r.StudentNo
WHERE `StudentResult` >= 80 AND `SubjectNo`= (
		SELECT SubjectNo FROM `subject` 
		WHERE `SubjectName` = '高等数学-2'
)

-- 再改造（由里及外）
-- 查询课程为高等数学-2 且 分数不小于80分的同学的学号和姓名
SELECT s.StudentNo, StudentName FROM student  WHERE StudentNo IN (
	SELECT StudentNo FROM result WHERE StudentResult>80 AND SubjectNo = (
		SELECT SubjectNo FROM `subject` WHERE `SubjectName` = '高等数学-2'
	)
)
```

### 4.7 分组和过滤
```
-- 查询不同课程的平均分，最高分，最低分
-- 核心：（根据不同的课程分组）
SELECT SubjectName, AVG(StudentResult) AS 平均分, MAX(StudentResult) AS 最高分, MIN(StudentResult) AS 最低分
FROM result r
INNER JOIN subject sub
ON r.SubjectNo = sub.SubjectNo
GROUP BY r.SubjectNo -- 通过什么字段来分组
HAVING 平均分>80
```

### 4.8 select小结
> 顺序很重要：
> select 去重 要查询的字段 from 表（注意：表和字段可以取别名）
> xxx join 要连接的表 on 等值判断
> where 具体的值，子查询语句
> group by 通过哪个字段来分组
> having 过滤分组后的信息，条件和where是一样的，位置不同
> order by 通过哪个字段排序 升序/降序
> limit startindex, pagesize 

> 业务层面
> 查询：跨表，跨数据库

## 5. MySQL 函数
### 5.1 常用函数
```

-- ======================常用函数=====================
-- 数学运算
SELECT ABS(-8) -- 绝对值
SELECT CEILING(9.4) -- 向上取整
SELECT FLOOR(9.4) -- 向下取整 
SELECT RAND() -- 返回一个0-1之间的随机数
SELECT SIGN(4) -- 判断一个数的符号  0-0 负数返回-1 整数返回1


-- 字符串函数
SELECT CHAR_LENGTH('即使再小的帆也能远航') -- 字符串长度
SELECT CONCAT('i','love','you') -- 拼接字符串
SELECT INSERT('我爱编程helloworld',1,2,'超级') -- 插入，从某个位置开始替换某个长度
SELECT LOWER('ADC') -- 字符串转小写
SELECT UPPER('abd') -- 字符串转大写
SELECT INSTR('kuangshen','h') -- 返回第一次出现的子串的索引
SELECT REPLACE('kuangshen','shen','nan') -- 替换出现的指定字符串
SELECT SUBSTR('狂神说坚持就能成功',4,6) -- 返回指定的子字符串(源字符串，截取的起始位置，截取长度)
SELECT REVERSE('冯绍峰') -- 反转字符串

-- 查询姓周的同学，名字  邹
SELECT REPLACE(studentName,'周','邹') FROM student
WHERE studentName LIKE '周%'

-- 时间和日期函数（记住）
SELECT CURRENT_DATE() -- 获取当前日期
SELECT CURDATE() -- 获取当前日期
SELECT NOW()  -- 获取当前时间
SELECT LOCALTIME()  -- 获取本地时间
SELECT SYSDATE() -- 获取系统时间

SELECT YEAR(NOW())
SELECT MONTH(NOW())
SELECT DAY(NOW())
SELECT HOUR(NOW())
SELECT MINUTE(NOW())
SELECT SECOND(NOW())


-- 系统
SELECT SYSTEM_USER()
SELECT USER()
SELECT VERSION()
```
### 5.2 聚合函数

| 函数名称  | 描述  |
|:----------|:----------|
| COUNT()    | 计数    |
| SUM()    | 求和    |
| AVG()    |平均    |
| MAX()    | 最大    |
| MIN()    | 最小    |


### 5.3 数据库级别的MD5加密（扩展）
什么是MD5?
> 主要增强算法复杂度和不可逆性。
> MD5不可逆，具体的值和md5是一样的
> MD5破解网站的原理，背后有一个字典，MD5加密后的值，加密前的值

```
CREATE TABLE `testmd5` (
		`id` INT(4) NOT NULL,
		`name` VARCHAR(20) NOT NULL,
		`pwd` VARCHAR(50) NOT NULL,
		PRIMARY KEY(`id`)
)ENGINE=INNODB DEFAULT CHARSET=utf8

-- 铭文密码
INSERT INTO testmd5 VALUES(1,'zhangshan','123456'),(2,'lisi','123456'),(3,'wangwu','123456')

-- 加密
UPDATE  testmd5 SET pwd=MD5(pwd) WHERE id = 1
UPDATE  testmd5 SET pwd=MD5(pwd) -- 加密全部的密码

-- 插入的时候加密
INSERT INTO testmd5 VALUES(4,'xiaomign',MD5('123456'))

-- 如何校验：将用户传递进来的密码，进行MD5加密，然后比对的加密后的值
SELECT * FROM testmd5 WHERE `name` = 'xiaomign' AND pwd = MD5('123456')

```

## 6、事务
### 6.1、什么是事务
要么都成功、要么都失败
===================
1、SQL执行 A给B转账 A 1000 -> 200 B 200

2、SQL执行 B收到A的钱 A 800 -> B 400

------------
将一组Sql放在一个批次中去执行
> 事务原则：ACID原则  原子性、一致性、隔离性、持久性  （脏读、幻读...）

原子性（atomicity）:要么都成功，要么都失败

一致性（consistency）:事务前后的数据完整性要保证一致

持久性（durability）：事务一旦提交将不可逆，被持久化到数据库中

隔离性（islation）:事务的隔离性是多个用户并发访问数据库时，数据库为每一个用户开启的事务，不能被其他事务的操作数据所干扰，事务之间要相互隔离

> 隔离所导致的一些问题
脏读：指一个事务读取了另外一个事务未提交的数据

不可重复读：在一个事务内读取表中的某一行数据，多次读取结果不同。（这个结果不一定是错误的，只是某些场合不对）

幻读：在一个事务内读取到了别的事务插入的数据，导致前后读取不一致







