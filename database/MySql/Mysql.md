## 数据库概念

数据库(database, DB)是一个长期存储在计算机内的,有组织的,有共享的,统一管理的数据集合.它是一个按数据结构来存储和管理数据的计算机软件系统.数据库包含两层含义:保管数据的"仓库",以及数据管理的方法和技术.

- 特点:实现数据共享,减少数据冗余;采用特定的数据类型;具有较高的数据独立性;具有统一的数据控制功能



### 表

在关系数据库中,数据库表是一系列二维数组的集合,用来存储数据和操作数据的逻辑结构.它由纵向的列和横向的行组成.**行被称为记录**,是组织数据的单位;**列被称为字段**,每一列表示记录的一个属性,有相应的描述信息,如数据结构,数据宽度等.



### 主键

主键(Primary Key)又称主码,用于唯一地址标识表中的每一条记录.可以定义表中的一列或多列为主键,主键列上既不能有两行相同的值,也不能为空值.



### SQL语言

对数据库进行查询和操作的语言叫做SQL.SQL的含义是结构化查询语言(Structured Query Language).包括以下四部分:

- 数据定义语言(DDL):   DROP、CREATE、ALTER等语句
- 数据操作语言(DML): INSERT、UPDATE等
- 数据查询语言(DQL):  SELECT
- 数据控制语言(DCL): GRANT、REVOKE等



##　MySQL

MySQL是一个小型跨平台的开源关系型数据库管理系统，与其他大型数据库管理系统（Oracle、DB2)相比，规模性功能有限，但是体积小、速度快、成本低，并且提供的功能对稍微复杂的应用来说已经够用。

从MySQL8开始，系统表全部换成事务性的InnoDB表 

​	

### 约束条件

- 主键约束：主键，又称主码，是表中一列或多列的组合。**主键约束要求主键的数据唯一，并且不允许为空**。主键能够唯一的标识表中的一条记录，可以结合外键来定义不同数据表之间的关系，并且可以加快数据库查询的速度。主键分为两种类型：单字段主键和多字段联合主键

  - 单字段主键：在定义列的同时指定主键或者在定义完所有列之后指定主键

    > id    INT(11)    PRIMARY  KEY,
    >
    > 或
    >
    > PRIMARY  KEY(id)

  - 多字段联合主键：使用后name和deptID成为联合主键

    >  PRIMARY KEY(name, deptID)

    ​				

- 外键约束：外键用来在两个表的数据之间建立连接，可以是一列或多列。一个表可以有一个或多个外键。外键对应的是参照完整性，一个表的外键可以是空值，若不为空值，则每一个外键值必须等于另一个表中主键的某个值。首先是表中的一个字段，虽然**可以不是主键**，但要对应另外一个表的主键，**定义后不允许删除在另一个表中具有关联关系的行**。外键约束不能跨引擎使用。

  > CONSTRAINT  <外键名> FORIGN KEY(字段名)   REFERENCES  <主表名>  主键列

  ​		

- 非空约束：指定字段的值不能为空

  > 字段名   数据类型   not  null

  ​		

- 唯一性约束：要求该列唯一，允许为空，但只能出现一个空值。唯一性约束可以确保一列或几列不出现重复值

  > 字段名   数据类型   UNIQUE

  和主键约束的区别：声明为PRIMARY的列不允许有空值，一个表中只能有一个声明。

  ​								   声明为UNIQUE的允许空值存在，可以有多个字段声明

  ​	

- 默认约束：指定某列的默认值

  > 字段名  数据类型  DEFAULT 默认值





### 基本操作

- 登录：                       mysql   -u username  -h hostname -p 
- 查看所有存在的数据库： SHOW DATABASE；
- 创建数据库：                    CREATE DATABASE  database_name;
- 删除数据库：                    DROP DATABASE  database_name;
- 选中数据库：                    USE database_name;
- 查看当前正在使用的库：  SELECT  DATABASE();



### 数据表

在数据库中，数据表是数据库中最重要，最基础的操作对象，是数据存储的基本单元。数据表被定义为列的集合，数据在表中是按照行和列的格式来存储的。每一行代表一条唯一的记录，每一列代表记录中的一个域。

- 创建表 

  > CREATE TABLE <表名>
  >
  > (
  >
  > ​	字段名1，  数据类型  [列级别约束条件] [默认值]，
  >
  > ​	字段名1，  数据类型  [列级别约束条件] [默认值]，
  >
  > ​	...
  >
  > ​	[表级别约束条件]
  >
  > )；



- 查看创建表语句

  > SHOW  CREATE  TABLE  <表名>

  ​		

- 设置表的属性值自动增加

  通过为主键添加AUTO_INCREMENT关键字，在每次插入新记录时，系统自动生成字段的主键值。初始值是1，每新增一条记录，字段值自动加1。一个表只能有一个字段使用AUTO_INCREMENT约束，且该字段必须为主键的一部分

  > 字段名  数据类型  AUTO_INCREMENT

  ​	

- 查看数据表结构

  > DECREIBE 表名
  >
  > 或
  >
  > DESC  表名

  ​		

- 修改数据表

  - 修改表名 ：  					ALTER  TABLE   <旧表名>  RENAME <新表名>

  - 修改字段数据类型：        ALTER  TABLE   <表名>  MODIFY  <字段名> <数据类型>

  - 修改字段名：                   ALTER   TABLE   <表名>   CHANGE <旧字段名> <新字段名> <新数据类型>

  - 添加字段：                       ALTER   TABLE   <表名>    ADD   <新字段名> <数据类型>  [约束条件] [FIRST|AFTER 已存在字段名]

  - 删除字段：                       ALTER   TABLE   <表名>   DROP   <字段名>

  - 修改字段排列位置：        ALTER   TABLE   <表名>    MODIFY  <字段1>  <数据类型>  FIRST|AFTER <字段2>

  - 更改表的存储引擎：        ALTER   TABLE   <表名>    ENGINE=<更改后的存储引擎名>

  - 删除表的外键约束：        ALTER   TABLE   <表名>   DROP  FOREIGN   KEY  <外键约束名>

  - 插入数据：                       INSERT  INTO      <表名>  <指定字段集合>  value (指定字段值) 

    ​	

- 删除表

  - 删除没有被关联的表：       DROP  TABLE  [IF EXISTS]  表1， 表2，...表n

  - 删除被其他表关联的主表：如果直接删除父表，会显示失败，因为会破坏表的完整性。可以先删除子表再删除父表，或者删除关联表的外键约束。

    ​			   
  
  
  
  

### 数据类型和运算符

 