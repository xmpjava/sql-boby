# 1 DDL

## 1.1  显示所包含的数据库

```mysql
SHOW DATABASES;
```

## 1.2  创建数据库

```mysql
CREATE DATABASE db2;
CREATE DATABASE IF NOT EXISTS db2;
```

## 1.3  删除数据库

```mysql
DROP DATABASE db2;
drop DATABASE IF EXISTS db2;
```

-- 查看当前所使用的数据库

```mysql
SELECT DATABASE();
```

## 1.4 使用数据库

```mysql
use db1;
```

### 1.4.1  创建表

<!--创建表，表中有字段名、字段名的类型、字段名长度、是否为空、是不是主键等等-->

<img src="https://gitee.com/love-code-bear/java/raw/master/img/sqlimg/create table.png" alt="create table" style="zoom:50%;" />

```mysql
CREATE TABLE jd_user(
id int,
username VARCHAR(32),
password VARCHAR(32)
);
```

### 1.4.2 查看表的结构

<!--展示表的结构（构成）-->

<img src="https://gitee.com/love-code-bear/java/raw/master/img/sqlimg/desc table.png" alt="desc table" style="zoom:50%;" />

```mysql
DESC stu;
```

### 1.4.3 查看当前数据库下的所有表

<!--展示数据库下表的名称-->

<img src="https://gitee.com/love-code-bear/java/raw/master/img/sqlimg/show table.png" alt="show table" style="zoom:50%;" />

```mysql
USE DATABASE db1;
SHOW TABLES;
```

### 1.4.4  基础的增删改查

#### 1.4.4.1  删除表

```mysql
DROP TABLE tb_user;
DROP TABLE IF EXISTS tb_user;
```

#### 1.4.4.2  添加列

```mysql
ALTER TABLE jd_user ADD address VARCHAR(32);
```

#### 1.4.4.3  修改表名

```mysql
ALTER TABLE jd_user RENAME TO jd_user;
```

#### 1.4.4.4  修改数据类型

```mysql
ALTER TABLE jd_user MODIFY address CHAR(32);
DESC jd_user;
```

#### 1.4.4.5  修改列名和数据类型

```mysql
ALTER TABLE jd_user CHANGE address location VARCHAR(64);
```

1.4.5  查询所有数据

```mysql
SELECT * FROM jd_user;
SELECT * FROM stu;
```

# 2 DML

## 2.1  给指定列添加数据

### 2.1.1  修改中文列的编码格式(修改列名和数据类型)：

```mysql
alter table stu change name name varchar(255) character set utf8;
INSERT INTO stu(id,name) VALUES(1,'张三');
```

### 2.1.2  给所有列添加数据

```mysql
alter table stu change sex sex varchar(255) character set utf8;
INSERT INTO stu(id,name,sex,birthday,score,email,tel,status) VALUES
(2,'lisa','女','1999-11-11',98.00,'1@qq.com',1123,1);
```

### 2.1.3  给所有列添加数据，列名的列表可以省略

```mysql
INSERT INTO stu VALUES(3,'小米','男','1998-10-17',93.00,'2@qq.com',1433,1);
```

### 2.1.4  批量添加

```mysql
INSERT INTO stu VALUES
(4,'huawei','男','1998-10-17',93.00,'2@qq.com',1433,1),
(5,'荣耀','男','1998-10-17',93.00,'2@qq.com',1433,1),
(6,'苹果','男','1998-10-17',93.00,'2@qq.com',1433,1);
```

## 2.2 修改数据

### 2.2.1 将张三的性别改为男

```mysql
UPDATE stu SET sex = '男' WHERE name = '张三';
```

### 2.2.2  将张三的生日改成2000-02-28，成绩改成99.00

```mysql
UPDATE stu SET birthday = '2000-02-28',score = '99.00' WHERE name = '张三';
```

### 2.2.3  如果update语句没有where条件，则表中的数据全部都被修改

## 2.3  删除数据

### 2.3.1 删除小米记录

```mysql
DELETE FROM stu WHERE name = '小米';
```

## 2.4 简单的创建表，添加数据，查询数据

-- 使用数据库
USE db1;
-- 创建表

```mysql
CREATE TABLE stu1 (
id int,
name VARCHAR(32),
age int,
sex VARCHAR(4),
address VARCHAR(64),
math DOUBLE(5,2),
english DOUBLE(5,2),
hire_date DATE
);
```

-- 插入数据

```mysql
ALTER TABLE stu1 CHANGE name name VARCHAR(32) character set utf8;
ALTER TABLE stu1 CHANGE sex sex VARCHAR(4) character set utf8;
ALTER TABLE stu1 CHANGE address address VARCHAR(64) character set utf8;
INSERT INTO stu1(id,name,age,sex,address,math,english,hire_date) 
VALUES
(1,'张一',25,'男','杭州',66.00,78.00,'1998-09-09'),
(2,'张二',24,'女','北京',87.00,76.00,'1996-09-09'),
(3,'张三',22,'男','郑州',94.00,65.00,'1997-09-09'),
(4,'张四',23,'男','合肥',69.00,75.00,'1998-09-09'),
(5,'张五',23,'女','无锡',76.00,79.00,'1999-09-09'),
(6,'张六',24,'女','苏州',88.00,94.00,'1998-03-09'),
(7,'张七',21,'男','南通',89.00,90.00,'1998-05-09'),
(8,'张八',22,'男','南充',98.00,90.00,'1998-07-09');
```

-- 查询所有数据

```mysql
SELECT * FROM stu1;
USE db1;
```

# 3 DQL

## 3.1  基础查询

### 3.1.1  查询所有列的数据，列名的列表可以使用*代替

```mysql
SELECT *FROM stu1;
SELECT `name`,age,sex,address,math,english,hire_date FROM stu1;
```

### 3.1.2 查询name age 两列

```mysql
SELECT `name`,age FROM stu1;
```

### 3.1.3  查询英语分数

```mysql
SELECT english FROM stu1;
```

### 3.1.4  去除重复记录

```mysql
SELECT DISTINCT english FROM stu1;
```

### 3.1.5  查询时起别名  as

```mysql
SELECT name AS 姓名,math AS 数学,english AS 英语 FROM stu1;
```

## 3.2  条件查询

### 3.2.1  查询年龄大于23岁的学员信息

```mysql
SELECT * FROM stu1	WHERE age > 23;
```

### 3.2.2 查询年龄>=24岁的学员信息

```mysql
SELECT * FROM stu1 WHERE age >= 24;
```

### 3.2.3  查询21<=年龄<=23岁的学员信息

```mysql
SELECT * FROM stu1 WHERE age>=21 AND age <= 23;
SELECT * FROM stu1 WHERE age BETWEEN 21 AND 23;
```

### 3.2.4  查询入学时间在1997-05-09--1998-07-09之间的学员信息

<!-- BETWEEN AND -->

```mysql
SELECT * FROM stu1 WHERE hire_date BETWEEN '1997-05-09' AND '1998-07-09';
```

### 3.2.5  查询年龄等于21岁的学员信息

```mysql
SELECT * FROM stu1 WHERE age = 21;
```

### 3.2.6 查询年龄等于21岁或者年龄等于24岁或者年龄等于25岁的学员信息

<!-- OR -->

```mysql
SELECT * FROM stu1 WHERE age = 21 OR age = 24 OR age = 25;
SELECT * FROM stu1 WHERE age IN(21,24,25);
```

### 3.2.7  查询英语成绩为空null的学员信息

<!-- 注意： null值的比较不能使用 = != .需要使用 is is not--> 

```mysql
SELECT * FROM stu1 WHERE english IS NOT null;
```

## 3.3  模糊查询

<!-- _代表单个任意字符，%代表多个任意字符-->

### 3.3.1  查询姓'张'的学员信息

```mysql
SELECT * FROM stu1 WHERE `name` LIKE '张%';
-- 查询第二个字是'三'的学员信息
SELECT * FROM stu1 WHERE `name` LIKE '_三%';
-- 查询名字中含有'四'的学员信息
SELECT * FROM stu1 WHERE `name` LIKE '%四%';
```

## 3.4 排序查询

<!-- ASC升序排列(默认)  DESC降序排列-->

### 3.4.1 查询学生信息,按照年龄升序排列

<!-- ORDER BY -->

```mysql
SELECT * FROM stu1 ORDER BY age ASC;
```

### 3.4.2 查询学生信息,按照数学成绩降序排列

```mysql
SELECT * FROM stu1 ORDER BY math DESC;
```

### 3.4.3 查询学生信息,按照英语成绩降序排列,如果英语成绩一样,再按照数学成绩升序排列

```mysql
SELECT * FROM stu1 ORDER BY english DESC , math ASC;
```

## 3.5 分组查询

 <!-- null 不参与聚合函数的运算 -->

### 3.5.1 聚合函数

#### 3.5.1.1 统计班级有多少个学生

<!-- COUNT -->

```mysql
SELECT COUNT(id) FROM stu1;
SELECT COUNT(*) FROM stu1;
```

#### 3.5.1.2 查询数学成绩最高分

<!-- MAX(字段名) -->

```mysql
SELECT MAX(math) FROM stu1;
```

#### 3.5.1.3 查询数学成绩最低分

<!-- MIN(字段名) -->

```mysql
SELECT MIN(math) FROM stu1;
```

#### 3.5.1.4 查询数学成绩总分

<!-- SUM(字段名) -->

```mysql
SELECT SUM(math) FROM stu1;
```

#### 3.5.1.5  查询数学成绩平均分

<!-- AVG(字段名) -->

```mysql
SELECT AVG(math) FROM stu1;
```

### 3.5.2 分组函数 

#### 3.5.2.1  查询男同学和女同学的各自平均分

<!-- GROUP BY -->

```mysql
SELECT sex,AVG(math) FROM stu1 GROUP BY sex;
```

#### 3.5.2.2 查询男同学和女同学的各自平均分,以及各自人数

```mysql
SELECT sex,AVG(math),COUNT(*) FROM stu1 GROUP BY sex;
```

#### 3.5.2.3 查询男同学和女同学的各自平均分,以及各自人数,要求分数低于80的不参与分组

```mysql
SELECT sex,AVG(math),COUNT(*) FROM stu1 WHERE math > 80 GROUP BY sex;
```

#### 3.5.2.4 查询男同学和女同学的各自平均分,以及各自人数,要求分数低于80的不参与分组,分组之后人数大于2

<!-- HAVING 条件 -->

```mysql
SELECT sex,AVG(math),COUNT(*) FROM stu1 WHERE math > 80 GROUP BY sex HAVING COUNT(*) > 2;
```

## 3.6 分页查询

```mysql
SELECT * FROM  stu1;
```

### 3.6.1  从0开始查询,查询第一页数据

<!-- LIMIT num,num -->

<!-- 起始数据，到终点位置，从0开始，按照num+num -->

```mysql
SELECT  * FROM stu1 LIMIT 0,3;
```

### 3.62  每页显示3条数据显示第一页

```mysql
SELECT  * FROM stu1 LIMIT 0,3;
```

### 3.6.3  每页显示3条数据显示第二页 

<!-- LIMIT num+num,num -->

```mysql
SELECT  * FROM stu1 LIMIT 3,3;
```

### 3.6.4  每页显示3条数据显示第三页

```mysql
SELECT  * FROM stu1 LIMIT 6,3;
```

### 3.6.5 每页显示4条数据显示第二页

```mysql
SELECT  * FROM stu1 LIMIT 4,4;
```

## 3.7  约束

### 3.7.1 字段的约束

<!-- 符合规范可以被插入  -->

```mysql
-- 员工表
CREATE TABLE emp(
id INT PRIMARY KEY,/*员工id主键，且自增长*/
ename VARCHAR(32) UNIQUE,/*员工姓名，非空且唯一*/
joindate DATE NOT NULL,/*入职日期非空*/
salary DOUBLE(7,2) NOT NULL,/*薪水，非空*/
bonus DOUBLE(7,2) DEFAULT 0/*奖金，默认为0*/
);
DESC emp;
ALTER TABLE emp CHANGE ename ename VARCHAR(32) CHARACTER set utf8;
INSERT INTO emp(id,ename,joindate,salary,bonus) VALUES(1,'张三','1999-11-11',8800,5000);
SELECT * FROM emp;
```

### 3.7.2 演示主键约束，非空且唯一

<!-- 添加数据时设置的主键不能为空 -->

```mysql
INSERT INTO emp(id,ename,joindate,salary,bonus) VALUES(NULL,'张三','1999-11-11',8800,5000);
INSERT INTO emp(id,ename,joindate,salary,bonus) VALUES(1,'张三','1999-11-11',8800,5000);
INSERT INTO emp(id,ename,joindate,salary,bonus) VALUES(2,'李四','1999-11-11',8800,5000);
```

### 3.7.3 演示非空约束

<!--被非空约束的字段名不能为空-->

```mysql
DELETE FROM emp WHERE id = 3;
INSERT INTO emp(id,ename,joindate,salary,bonus) VALUES(3,null,'1999-11-11',8800,5000);
```

### 3.7.4  演示唯一约束

<!-- 被唯一约束的字段名，插入数据时不能重复 -->

```mysql
INSERT INTO emp(id,ename,joindate,salary,bonus) VALUES(3,'李四','1999-11-11',8800,5000);
```

### 3.7.5 对约束的操作

#### 3.7.5.1 删除约束

<!-- 将原本有约束的字段名约束直接设为空 -->

```mysql
ALTER TABLE emp MODIFY ename VARCHAR(32) CHARACTER set utf8;
```

#### 3.7.5.2 添加约束

<!-- xxxxxx NOT NULL -->

```mysql
ALTER TABLE emp MODIFY ename VARCHAR(32) NOT NULL ;
DESC emp;
DROP TABLE emp;
```

#### 3.7.5.3 外键约束（实例演示）

```mysql
-- 员工表
CREATE TABLE emp(
id INT PRIMARY KEY auto_increment,/*员工id主键，且自增长*/
name VARCHAR(32),/*员工姓名，非空且唯一*/
age INT,
dep_id INT,/*联系到拎一个表*/
-- 添加一个外键约束
CONSTRAINT fk_emp_dept FOREIGN KEY(dep_id) REFERENCES dept(id)
);
-- 部门表
CREATE TABLE dept(
id INT PRIMARY KEY auto_increment,
dep_name VARCHAR(32),
address VARCHAR(32)
);
DESC emp;
DESC dept;
DROP TABLE emp;
DROP TABLE dept;
ALTER TABLE emp CHANGE name name VARCHAR(32) CHARACTER set utf8;
ALTER TABLE dept CHANGE dep_name dep_name VARCHAR(32) CHARACTER set utf8;
ALTER TABLE dept CHANGE address address VARCHAR(32) CHARACTER set utf8;
INSERT INTO emp (name,age,dep_id) VALUES
('张三',20,1),
('李四',20,1),
('王五',20,1),
('赵六',20,2),
('孙七',22,2),
('周八',18,2);
INSERT INTO dept (dep_name,address) VALUES
('研发部','广州'),
('销售部','深圳');
SELECT * FROM emp;
SELECT * FROM dept;
-- 删除外键
ALTER TABLE emp DROP FOREIGN KEY fk_emp_dept;
-- 添加外键
ALTER TABLE emp ADD CONSTRAINT fk_emp_dept FOREIGN KEY(dep_id) REFERENCES dept(id);
```

# 4 外键

使用数据库，展示所有表

```mysql
USE db1;
SHOW TABLES;
```

## 4.1 外键的建立

### 4.1.1 多对多关系

```mysql
-- 订单表
CREATE TABLE tb_order(
id INT PRIMARY KEY auto_increment,
payment double(10,2),
payment_type TINYINT,
status TINYINT
);
-- 商品表
CREATE TABLE tb_goods(
id INT PRIMARY KEY auto_increment,
title VARCHAR(100),
price DOUBLE(10,2)
);
-- 中间表
CREATE TABLE tb_order_goods(
id INT PRIMARY KEY auto_increment,
order_id INT,
goods_id INT
);
-- 添加外键
ALTER TABLE tb_order_goods ADD CONSTRAINT fk_order_id FOREIGN KEY(order_id) REFERENCES tb_order(id);
ALTER TABLE tb_order_goods ADD CONSTRAINT fk_goods_id FOREIGN KEY(goods_id) REFERENCES tb_goods(id);
SHOW TABLES;
```



### 4.1.2 一对一关系

```mysql
-- 用户表
CREATE TABLE tb_user(
id INT PRIMARY KEY auto_increment,
photo VARCHAR(100),
name VARCHAR(32),
age INT,
sex VARCHAR(4),
desc_id INT UNIQUE,
CONSTRAINT tb_user_desc FOREIGN KEY(desc_id) REFERENCES tb_user_desc(id) 
);
-- 用户详情表
CREATE TABLE tb_user_desc(
id INT PRIMARY KEY auto_increment,
city VARCHAR(32),
edu VARCHAR(32),
income DOUBLE(7,2),
status TINYINT
);
ALTER TABLE tb_user_desc CHANGE status status VARCHAR(16) CHARACTER set utf8;
INSERT into tb_user_desc(city,edu,income,status) VALUES
('广州','本科',3000,'单身'),
('广州','硕士',12000,'单身');
INSERT into tb_user(photo,`name`,age,sex,desc_id) VALUES
('c盘','林青霞',22,'女',1),
('d盘','风清扬',24,'男',2);
ALTER TABLE tb_user auto_increment = 1;
SELECT * FROM tb_user;
SELECT * FROM tb_user_desc;
DESC tb_user;
DESC tb_user_desc;
DROP TABLE tb_user;
```

4.1.3 查看所有外键

```mysql
SELECT * FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE;
```

## 4.2 实例演示练习

```mysql
-- 音乐专辑表名
CREATE TABLE music(
title VARCHAR(32),/*专辑名*/
alias VARCHAR(32),/*专辑别名*/
image VARCHAR(64),/*封面图片*/
style VARCHAR(16),/*流派（经典、流行、民谣）*/
type VARCHAR(8),/*类型（专辑，单曲）*/
medium VARCHAR(8),/*介质（胶片，cd）*/
publish_time DATE,/*发行时间*/
publisher VARCHAR(8),/*出版者*/
number TINYINT,/*唱片数量*/
barcode BIGINT,/*条形码*/
summary VARCHAR(1024),/*简介*/
artist VARCHAR(32),/*艺术家*/
id INT UNIQUE/*编号，唯一*/
);
-- 曲目表名
CREATE TABLE song(
name VARCHAR(32),/*歌曲名*/
serial_number TINYINT,/*歌曲序号*/
id INT UNIQUE/*编号，唯一*/
);
-- 评论表名
CREATE TABLE review(
content VARCHAR(1024),/*评论内容*/
rating TINYINT,/*评分1-5*/
review datetime,/*评论时间*/
content_user_id INT,
content_music_id INT
);
-- 用户表名
CREATE TABLE user(
username VARCHAR(32),
image VARCHAR(64),
signture VARCHAR(64),
name VARCHAR(32),
id INT PRIMARY KEY
);
-- 展示
DESC music;
DESC song;
DESC review;
DESC user;
-- 删除
DROP TABLE music;
DROP TABLE song;
DROP TABLE review;
DROP TABLE user;
-- 专辑和用户的中间表
CREATE TABLE music_user(
id INT PRIMARY KEY auto_increment,
music_id INT,
user_id INT
);
-- 添加专辑和用户外键
ALTER TABLE music_user ADD CONSTRAINT fk_music_id FOREIGN KEY(music_id) REFERENCES music(id);
ALTER TABLE music_user ADD CONSTRAINT fk_user_id FOREIGN KEY(user_id) REFERENCES user(id);
-- 添加短评和用户外键
ALTER TABLE review ADD CONSTRAINT fk_review_user FOREIGN KEY(content_user_id) REFERENCES user(id);
-- 添加短评专辑外键
ALTER TABLE review ADD CONSTRAINT fk_review_music FOREIGN KEY(content_music_id) REFERENCES music(id);
-- 添加曲目和专辑外键
ALTER TABLE song ADD CONSTRAINT fk_song_music FOREIGN KEY(id) REFERENCES music(id);
ALTER TABLE song DROP FOREIGN KEY fk_song_user;
```

### 逆向化模型

<img src="https://gitee.com/love-code-bear/java/raw/master/img/sqlimg/music.png" alt="music" style="zoom:50%;" />

-- 多表查询

```mysql
SELECT * FROM emp;
SELECT * FROM dept;
SELECT * FROM emp,dept;
```

-- 产生笛卡尔积（有ab两个集合，去a和b所有的组合情况）
-- 消除无效数据
-- 查询emp和dept的数据，emp.dep_id = dept.id
-- 隐式内连接

```mysql
SELECT * FROM emp,dept WHERE emp.dep_id = dept.id;
```

-- 查询emp的name,age，dept表的dep_name

```mysql
SELECT emp.`name`,emp.age,dept.dep_name FROM emp,dept WHERE emp.dep_id = dept.id;
```

-- 给表起别名

```mysql
SELECT t1.`name`,t1.age,t2.dep_name FROM emp AS t1,dept AS t2 WHERE t1.dep_id = t2.id;
```

-- 显式内连接

```mysql
SELECT * FROM emp LEFT OUTER JOIN dept ON emp.dep_id = dept.id;
SELECT * FROM emp LEFT /*OUTER*/ JOIN dept ON emp.dep_id = dept.id;
```

-- 右外连接

```mysql
SELECT * FROM emp RIGHT OUTER JOIN dept ON emp.dep_id = dept.id;
SELECT * FROM emp RIGHT /*OUTER*/ JOIN dept ON emp.dep_id = dept.id;
```