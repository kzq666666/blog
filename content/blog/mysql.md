---
title: "Mysql"
date: 2018-10-30T17:06:30+08:00
showDate: true
draft: false
tags: ["数据库","关系型数据库","Mysql"]
---
mysql数据库是我今年暑假在家学习，当时学习的时候写了一些笔记，现在把笔记整理到博客上。

## 事务(ACID规则)
* 原子性(Atomicity)：多组操作为一个整体，不能分割，全部操作成功才算成功，有一步失败就失败了，一环扣一环。
* 一致性(Consistency)：操作前后最终的总量一样，比如说转账，两个人相互转账，这两个人无论向对方怎么转，两个人的总钱数是不变，如果变了，就说明失败了。
* 隔离性(Isolation)：并发(都在进行的)事务之间相互隔离互不干扰。
  
    <br>（1）在mysql中事务有4种隔离级别：`read uncommitted(读取未提交)`、`read committed(读取提交)`、`repeatable read(可以重复读)`、`Serializable`
	<br>（2）查看mysql软件的事务隔离级别：`SELECT @@tx_isolation`;
	<br>（3）修改mysql软件默认的隔离级别：`set global transaction isolation level 隔离级别`
	<br>（4）不同的隔离级别会引发不同的问题：<br>当mysql事务的隔离级别为read uncommitted时，会引发脏读(一个事务可以读取另一个事务未提交的数据.),解决脏读问题可以将数据库事务的隔离级别改为:read committed
    <br>当mysql软件的事务隔离级别为:read committed的时候，会引发不可重复读：在同一事物中多次读取的结果不一致
    如何解决不可重复读：将事物的隔离级别改为repeatable read
    <br>当mysql软件的事务隔离级别为:repeatable read时，会引发虚读(幻读)
		
		
	
* 持久性(Durability)：数据进入到数据库中后，数据会持久存在




















```sql
DROP DATABASE kzq;

#在创建库时，希望制定编码 语法：create database库名 set 编码名
CREATE DATABASE kzq CHARACTER SET utf8;

#-----------------------------创建表（table）---------------------------------------------
#创建表语法：
CREATE TABLE 表名(
	字段1 数据类型 COMMENT .....,#注释 comment 。。。
	字段2 数据类型 COMMENT .....,
	.......
)
# 选中某一个数据库： use 库名；
USE kzq;
CREATE TABLE java成绩表(
	姓名 VARCHAR(40),
	班级 VARCHAR(20),
	Java成绩 FLOAT 
);
# 删除制定表语法：drop table 表名;
DROP TABLE java成绩表;

# ------------------------往表中添加、删除、修改、查询数据(CRUD)-------------------------------------------
#往置顶的表中添加数据：
#第一种方法 insert into 表名(字段1,字段2....) values(值1,值2)
INSERT INTO java成绩表 (姓名,班级,Java成绩) VALUES ('隔壁老王','g405班',90.5)
#在插入时，可以省略掉后面的字段名，但必须全

INSERT INTO java成绩表 VALUES ('隔壁老王','g405班',90.5)
#第二种方法 insert into 表名 set 字段名1=字段值1
INSERT INTO java成绩表 SET 姓名='李思';

#同时插入多条数据
INSERT INTO java成绩表 (姓名,班级,Java成绩) 
VALUES ('隔壁老王','g405班',90.5),('def','g405','90.6')

# 删除数据语法：delete from 表名 where 条件
# 如果“=“是放在set关键字后面，则是”赋值运算符“
# 如果“=”是放在where 关键字后，则是“关系运算符”
DELETE FROM java成绩表 WHERE 姓名='李思'


#-------------------关系运算符---------------------------
#在mysql中常用的关系运算符有：=、>、>=、<、<=、!=
#在mysql中关系运算符需要放置在where关键字之后
#查询语法规则：select 字段1，字段2....from 表名 (where 条件)
# 1、查询某一张表中的所有数据记录
SELECT 姓名,班级,java成绩 FROM Java成绩表;
SELECT 姓名 FROM Java成绩表;
SELECT * FROM java成绩表;#*代表查询某一张表中的所有字段
SELECT 姓名 (AS 及格人员) FROM java成绩表 WHERE java成绩>=60;

#------------逻辑运算符------------------
# 与and 或or 非not

#给表取别名

SELECT * FROM java成绩表 s;

#---------------------对表数据的增（create）删（delete）改（update）查（select）-------------------------------
#修改语法 ：update 表名 set 字段名1=值1.... where 条件
UPDATE java成绩表 SET 班级='1' WHERE 姓名='李思'

#删除
DELETE FROM java成绩表 WHERE 

#------------------------对sql语句进行分类--------------------------------------------
#数据库查询语言DQL（datebase query language）:对表的查询语句：select
#数据库定义语言DDL（datebase defined language）:create database、create table、drop datebase、drop table、
#数据库操作语言DML（database manage language）:update、insert、delete


#DDL之操作库
#添加数据库：create datebase 库名【character set utf8/gbk】
#删除指定的数据库：drop database 库名;
#查询指定库的详细信息：
	(1)SHOW CREATE DATABASE 库名;查看某一个数据库的详细信息
	SHOW CREATE DATABASE kzq;
	(2)SHOW DATABASES:查看mysql服务器软件下所有的库 
	(3)查看：当前用户连接的是哪个数据库：select DATABASE();
	(4)查看指定的数据库下有哪些表:SHOW TABLES;
	


#修改指定库的编码： alter database 库名 character set 新编码名;
ALTER DATABASE dt55_account CHARACTER SET utf8;
SHOW CREATE DATABASE dt55_account

#--------------------------DDL之对表的增删改查-----------------------------------
#创建一张表：
CREATE TABLE 表名(字段名 数据类型,字段名2 数据类型....);
#删除表： drop table 表名：

#查询：(1)、查询某一张表的结构：desc（description） 表名
		DESC bank;
	(2)、打印某一张表SQL创建信息： SHOW CREATE TABLE 表名;
		SHOW CREATE TABLE bank;
#修改表：
	(1) RENAME TABLE 旧表名 TO 新表名;
		RENAME TABLE aaa TO bank;
	(2) 添加字段：	ALTER TABLE 表名 ADD 字段名 数据类型;
		ALTER TABLE bank ADD gender VARCHAR(2);
	(3) 删除字段： ALTER TABLE 表名 DROP 被删除字段名;
		ALTER TABLE bank DROP gender;
	(4) 重命名字段 ALTER TABLE 表名 CHANGE 旧字段名 新字段名 新字段名数据类型;
		ALTER TABLE bank CHANGE usenames aaa VARCHAR(40);
	(5) 修改数据类型(长度) 
		ALTER TABLE bank CHANGE bankNo bankN0 VARCHAR(25);


# --------------------数据库的备份和还原----------------------------------
#第一种通过命令：mysqldump -u root -p (密码) 需要备份的数据库名>备份后的sql脚本名;
		cmd----->mysqldump -uu root -p (密码) dt55_account>c:\dt55_account_back.sql
	还原备份文件数据：进入mysql环境---->创建一个库---->在库下还原数据
		source 备份数据库脚本
#第二种通过sqlyog工具:选中需要备份的数据库----->右键------>备份/导出---->转储到sql


#删除指定表字段
ALTER TABLE 表名 DROP 字段名


#--------------------数据类型属性--------------------------------
#mysql常见的数据类型：varchar（n）、float、int(n)、bigint(n)、date、datetime、text
#默认值 default '默认值'
#非空：NOT NULL 如果某一个字段别NOT NULL修饰后，添加数据时，此字段必需填写
#自动整长：auto_increment，尽量作用在int类型的字段上
#主键(唯一的，不能重复，一张表中只能以一个作为主键)：primary key
#唯一健（唯一，可以有很多）：unique，被unique修饰的数据不能够重复
USE kzq;
DROP TABLE students;
CREATE TABLE students(
	id BIGINT(20) AUTO_INCREMENT PRIMARY KEY COMMENT '学生编号',
	stuName VARCHAR(40) COMMENT '学生姓名',
	gender VARCHAR(2) DEFAULT '男' COMMENT '性别',
	className VARCHAR(20) NOT NULL COMMENT '班级',
	phone VARCHAR(20) UNIQUE COMMENT '手机号码'
)
#此处的delete可以删除整张表，但是删除数据后，自增列不会从1开始
DELETE FROM students WHERE id=1	()

#如果要删除一整张表中的数据，使用truncate，使用truncate删除数据后，如果字段是自增的、则重新排列
TRUNCATE TABLE students;

#================================================================
USE dt55_account;
CREATE TABLE users(
	id BIGINT(20) NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT '用户编号',
	username VARCHAR(40) NOT NULL COMMENT '用户名',
	gender VARCHAR(2) DEFAULT '女' COMMENT '性别',
	idcard VARCHAR(20) UNIQUE NOT NULL COMMENT '身份证号',
	javaScore FLOAT DEFAULT '0' COMMENT 'java成绩'
)
INSERT INTO users SET username='关雨',gender='男',idcard='110',javaScore=90;
INSERT INTO users SET username='钱文雯',gender='男',idcard='120',javaScore=80;
INSERT INTO users SET username='文儿',gender='男',idcard='911',javaScore=70;


#---------------------------排序(order by 字段 降序，升序)---------------------------------------------
#降序(DESC)
SELECT * FROM users ORDER BY javaScore DESC;
#升序(ASC)
SELECT * FROM users ORDER BY javaScore ASC;
USE dt55_account;
RENAME DATABASE 'dt55_account' TO 'class'


#--------------------聚合函数-----------------------------
SELECT 函数名（字段） FROM 表名

#找出最大值：max(字段)
SELECT MAX(javaScore) AS 最高分 FROM users;

#找出最小值：min(字段)
SELECT MIN(javaScore) AS 最低分 FROM users;

#求平均数：avg(字段名)
SELECT AVG(javaScore) AS 平均分 FROM users;

#求和 sum
SELECT SUM(javaScore) AS 总分数 FROM users;

#统计记录 count
SELECT COUNT(*) FROM users

#------------------常用函数---------------------
SELECT NOW() 年月日、时分秒
SELECT CURTIME() 时分秒
SELECT CURDATE() 年月日

SELECT CEIL(2.3) 向上取舍
SELECT FLOOR(2.3) 向下取舍
SELECT RAND() 返回0到1的随机数


#-------------------同时查询多条记录------------------------
SELECT * FROM users WHERE id IN (1,3)
SELECT * FROM users WHERE id 


#分组查询group by 分类字段
#查询是否有种类为衣服的类型
SELECT goodcategory FROM goods GROUP BY goodcategory HAVING goodcategory='衣服'


#分页 limit 起始下标，每页显示的数据量
#goods表中有七条数据记录，每一页显示三条，总共可以分3页

#获取第一页数据
SELECT * FROM goods LIMIT 0,3;

#获取第二页数据
SELECT * FROM goods LIMIT 3,3;

#获取第三页的数据
SELECT * FROM goods LIMIT 6,3;


#复制某一张表
CREATE TABLE aaa(
	SELECT * FROM `bank`
);
#插入数据
INSERT INTO aaa SELECT * FROM kzq.`java成绩表` 


#时间格式函数
SELECT DATE_FORMAT(DATE,'%Y年%m月%d日 %H:%i:%s') AS birthday FROM persons
USE kzq
#多表查询
DROP dept
#部门表dept
CREATE TABLE dept(
	id BIGINT(20) NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT '部门编号',
	deptName VARCHAR(20) COMMENT '部门名称'
)
ID  deptName(部门名称)	
1	开发部
2	测试部
3	UI/前端部
4	销售部	 
#员工表emp
ID  empName(员工名字)	salary	deptID
1	光谷		8000	   1	
2	蔡光		8500	   1	
3	杨成全		9000       2
CREATE TABLE emp(
	id BIGINT(20) NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT '员工编号',
	empName VARCHAR(20) COMMENT '员工名',
	salary FLOAT COMMENT '薪水',
	deptId BIGINT(20) COMMENT '部门编号'
)

#查询部门dept编号=1的部门下的所有员工
SELECT * FROM emp WHERE deptId=2

#查询所有员工
SELECT d.deptname,e.empName,e.salary FROM dept d,emp e WHERE d.deptname IN ('开发部','测试部') AND d.id=e.deptid
SSSSs

UNION 可以将两个查询语句的结果进行合并，合并的前提是两个查询语句的数据结构是一样的(如果有两个相同的数据，则自动去重)
UNION ALL 不能去重、

#---------------------------------多表查询------------------------------------------
#多表查询语法1：select * from 表1,表2....表n where 条件
#多表查询方式：
	内连接
	外连接
		左右连接
		右外连接
#内连接：表1 inner join 表2 on 条件(多个表中有关联的条件)
#查询所有部门中的所有员工
SELECT * FROM dept d,emp e WHERE d.id = e.deptId
SELECT * FROM dept d INNER JOIN emp e ON d.id = e.deptId

SELECT d.deptName,e.empName,e.salary
FROM
dept d INNER JOIN emp e
ON d.id = e.deptId WHERE d.dept = '开发部' #on后面接几个表中有关联的条件，没有关联的条件用where

#模糊查询 like
a% 以a开头
%a 以a结尾
%a% 包含a # %占位符

#左外连接 left join 以左边的表为主，左边的表数据要显示出来
#右外连接 right join 以右边的表为主，右边的表数据要显示出来




#视图：在真实表上面构建的一张虚表 create view 视图名 as 查询语句;
CREATE VIEW view_all
AS SELECT e.empName,e.salary,d.deptname FROM dept d INNER JOIN emp e ON d.id = e.deptId;
.
DROP VIEW view_all;

视图的应用场景：在金融行业，保险行业，财务行业等


#数据库建模(powerDesinger)

#事务：多组操作要么全部，要么全部失败
#开启事务：
START TRANSACTION;

#回滚事务：
ROLLBACK;

#提交事务
COMMIT;

#事务的四大特性：
	#原子性：多组操作为一个整体，不能分割
	
	#一致性：操作前后最终的总量一样
	
	#隔离性：多个事务之间相互隔离互不干扰
	 #在mysql中事务有4种隔离级别：read uncommitted(读取未提交)、read committed(读取提交)、repeatable read(可以重复读)、Serializable
	 #查看mysql软件的事务隔离级别:select @@tx_isolation;
	 SELECT @@tx_isolation;
	  
	 
	 #修改mysql软件默认的隔离级别：set global transaction isolation level 隔离级别
	 SET GLOBAL TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;
	 
	 #不同的隔离级别会引发不同的问题：
		#当mysql事务的隔离级别为read uncommitted时，会引发脏读：一个事务可以读取另一个事务未提交的数据
		#如何解决脏读问题：可以将数据库事务的隔离级别改为:read committed
		SET GLOBAL TRANSACTION ISOLATION LEVEL READ COMMITTED;
		
		#----------------------------------------------------------
		#当mysql软件的事务隔离级别为:read committed的时候，会引发不可重复读：在同一事物中多次读取的结果不一致
		#如何解决不可重复读：将事物的隔离级别改为repeatable read
		SET GLOBAL TRANSACTION ISOLATION LEVEL REPEATABLE READ;
		
		#当mysql软件的事务隔离级别为:repeatable read时，会引发虚读(幻读)
		
		
	
	#持久性：数据进入到数据库中后，数据需要持久存在
	

#-------------------------------------存储过程-----------------------------------------------
#给员工加薪：加薪的金额(salary),员工编号(id)
public BOOLEAN addSalary(FLOAT money,INT id){
	代码块;
	RETURN TRUE;
}

#存储过程语法：
DELIMITER //
CREATE PROCEDURE 存储过程名(参数名1 参数类型1,参数名2 参数类型2)
BEGIN
	代码块;
END//
DELIMITER ;

#书写一个加薪的存储过程
#存储过程：是一组sql语句的集合
DELIMITER //
CREATE PROCEDURE addSalary(money FLOAT,idd BIGINT)
BEGIN
	UPDATE `emp` SET salary=salary+money WHERE id=idd;
END//
DELIMITER ;

#调用存储过程:call 存储过程名()
CALL `addSalary`(-1000,9);

#删除存储过程
DROP PROCEDURE 存储过程名;
DROP PROCEDURE `addSalary`;

#----------------------带返回值的存储过程-----------------------
#test1：传递两个float类型的形参，返回两个数的和
public FLOAT test1(FLOAT i,FLOAT j){
	FLOAT num = i+j;
	RETURN num;
}

DELIMITER //
CREATE PROCEDURE test1(IN i FLOAT,IN j FLOAT,OUT num FLOAT)
BEGIN
	SET num=i+j;
END//
DELIMITER ;

CALL `test1`(10,20,@result)
SELECT @result

#--------------------------------------mysql数据库高级部分之存储过程-----------------------------------------------------
#创建存储过程的基本语法规则：
DELIMITER //
CREATE PROCEDURE 存储过程名(IN 输入参数名 参数类型,OUT 输出参数名 参数类型)
BEGIN
	代码块;
END//
DELIMITER ;

#删除存储过程: 
DROP PROCEDURE 【if exists】 存储过程名;
DROP PROCEDURE IF EXISTS test1;

#调用存储过程
CALL 存储过程名(参数1...参数n);

#带if语句的存储过程
#加薪的存储过程，传递两个参数：id、m(只能够传递整数，不能够传递负数)
SELECT '亲，您输入的金额不能够为负数!!!' AS '友情提示';

DELIMITER //
CREATE PROCEDURE pro_addSalary(idd BIGINT,m FLOAT)
BEGIN
	IF m>0 THEN
		UPDATE users SET money=money+m WHERE id=idd;
	END IF;
END//
DELIMITER ;

CALL `pro_addSalary`(1,-500);

#带if..else的存储过程
DROP PROCEDURE IF EXISTS pro_salaryAdd;
DELIMITER //
CREATE PROCEDURE pro_salaryAdd(idd BIGINT,m FLOAT)
BEGIN
	IF m>0 THEN
		UPDATE users SET money=money+m WHERE id=idd;
	ELSE 
		SELECT '亲，您输入的金额不能够为负数!!!' AS '友情提示';
	END IF;
END//
DELIMITER ;

CALL `pro_salaryAdd`(1,-2000);

#带if...else if...else语句的存储过程
#存储过程名:pro_buyCar(money float)，如果money>500万则买保时捷；否则如果money>300万，买宝马；否则如果money>10万买奥拓；否则骑摩拜
DELIMITER //
CREATE PROCEDURE pro_buyCar(money FLOAT)
BEGIN
	IF money>500 THEN
		SELECT '买保时捷' AS '买啥';
	ELSEIF money>300 THEN
		SELECT '宝马' AS '买啥';
	ELSEIF money>10 THEN
		SELECT '奥拓' AS '买啥';
	ELSE
		SELECT '骑摩拜' AS '骑啥';
	END IF;
END//
DELIMITER ;

CALL `pro_buyCar`(5);

#练习题：存储过程:pro_score(score float)，如果成绩>90分则是A等；
#否则score>80B等；否则如果score>=60，C等；否则score<60，不及格


#case选择分支结构
#存储过程名:pro_case(i int)，如果i=1则打印星期一，i=2则打印星期二....
DELIMITER //
CREATE PROCEDURE pro_case(i INT)
BEGIN
	CASE i
		WHEN 1 THEN
			SELECT '星期一' AS '日期';
		WHEN 2 THEN
			SELECT '星期二' AS '日期';
		ELSE
			SELECT '今天不是周一或者周二，到底周几你猜？' AS '日期';
	END CASE;
END//
DELIMITER ;

CALL `pro_case`(3);

#case练习：存储过程名:pro_case2(i int)，
#如果i=1，则拨打"爸爸"的电话，如果i=2则拨打"妈妈",否则：您打错了
DELIMITER //
CREATE PROCEDURE pro_case2(i INT)
BEGIN
	CASE i
		WHEN 1 THEN
			SELECT '拨打father的号码';
		WHEN 2 THEN
			SELECT '拨打mother的号码';
		ELSE
			SELECT '您打错了';
	END CASE;
END//
DELIMITER ;

CALL `pro_case2`(1);



###while循环
#Java中while循环的语法:
WHILE(条件){
	循环体;
	循环终止条件;
}
#存储过程名：pro_while2(i int)，如果i=100，则计算1到100之间的所有数之和，返回最终结果
DELIMITER //
CREATE PROCEDURE pro_while2(IN i INT,OUT total INT)
BEGIN
	DECLARE a INT DEFAULT 1;
	SET total=0;
	WHILE a<=i DO
		SET total=total+a;
		SET a=a+1;
	END WHILE;
END//
DELIMITER ;

CALL `pro_while2`(100,@aaa);
SELECT @aaa;


#如果i=100则往users表中插入100条数据
DROP PROCEDURE IF EXISTS pro_while1;
DELIMITER //
CREATE PROCEDURE pro_while1(IN i INT)
BEGIN
	DECLARE a INT DEFAULT 1;
	WHILE a<=i DO
		INSERT INTO `users` SET username='test',money=100;
		SET a=a+1;
	END WHILE;
END//
DELIMITER ;

CALL pro_while1(10);
SELECT COUNT(*) FROM users;
TRUNCATE TABLE users;

##loop循环:
CREATE PROCEDURE 存储过程名()
BEGIN
	loop循环别名:LOOP
		循环体;
		
		LEAVE loop循环别名;
	END LOOP;
END;

#-----------------------
#通过loop循环往users表中同时添加100条记录
DELIMITER //
CREATE PROCEDURE pro_loop()
BEGIN
	DECLARE i INT DEFAULT 0;
	loop_test1:LOOP
		INSERT INTO `users` SET username='admin',money=200;
		
		SET i = i+1;
		IF i=100 THEN
			LEAVE loop_test1;
		END IF;
	END LOOP;
END//
DELIMITER ;

CALL `pro_loop`();

#------------------------找出1-100之间能够被3整除的所有数之和-----------------------------
DROP PROCEDURE IF EXISTS `pro_sum`;
DELIMITER //
CREATE PROCEDURE `pro_sum`()
BEGIN
	DECLARE i INT DEFAULT 1;
	DECLARE total INT DEFAULT 0;
	WHILE i<=10 DO
		IF i MOD 3=0 THEN
			SET total=total+i;
		END IF;
		SET i = i+1;#循环结束条件
	END WHILE;
	SELECT total;
END//
DELIMITER ;

CALL `pro_sum`();

#作业
#书写一个存储过程，将`users`表中的所有money之和返回
SELECT SUM(money) FROM `users`;
DELIMITER //
CREATE PROCEDURE pro_qiuSum(OUT total FLOAT)
BEGIN
	SELECT SUM(money) INTO total FROM `users`;
END//
DELIMITER ;

CALL pro_qiuSum(@a);
SELECT @a;


# 2018年7月30日11:57:32用scrapy爬取豆瓣top250电影并存入数据库的一些查询语句
USE kzq;
SELECT * FROM movies;
SELECT id,title AS 爱情电影,movie_type,score FROM movies WHERE movie_type LIKE '%爱情%';
SELECT * FROM movies ORDER BY number DESC;
SELECT id,title FROM movies WHERE country LIKE '%中国%'
SELECT COUNT(*) FROM (SELECT id,title FROM movies WHERE country LIKE '%中国%') AS a

SELECT COUNT(*) FROM movies
SELECT title,COUNT(*) FROM movies GROUP BY country 


获取电影类型中出现爱情的次数
SELECT SUM(CHAR_LENGTH(movie_type)-CHAR_LENGTH(REPLACE(movie_type,'爱情','')))/2 AS 剧情电影总数 
FROM movies;

另一种写法

SELECT COUNT(*) FROM 
(SELECT id,title FROM movies WHERE movie_type LIKE '%爱情%')AS a


```
