# hive框架

## 检查maven

1. 解压  tar zxvf apache-maven-3.0.5-bin.tar.gz -C /opt/module/

2. 配置maven_home

   配置环境变量

   vim /etc/profile

   export MAVEN_HOME=/opt/module/apache-maven-3.0.5
   export PATH=$PATH:$MAVEN_HOME/bin

   （$path 作用是可以使用相对路径，否则只能使用绝对路径）

3. 检查离线仓库 

   去网上下了个包解压了就行

4. 检查eclipse

   运行试试，简单配置

   在eclipse中配置MAVEN

5. 创建maven项目

# hive认识

它是一个数据仓库，不是数据库。

数据库与数据库的区别，和数据库之间有什么区别？

数据库：mysql 、Oracle 、sql 、db2、sqlite、mdb

数据仓库：hive（可以理解为MapReduce的客户端），也就是说不用每台机器都安装部署

## hive的工作流程

![](D:\BaiduNetdiskDownload\尚硅谷2018大数据全套（8月8更新版）\05_尚硅谷大数据技术之Hive框架基础\01_尚硅谷大数据技术之Hive框架基础一\5.hive课堂笔记\Hive之灵魂画手.png)

在mysql中生成metastore数据库；hive为什么要依赖某一个数据库，是因为hive要做一个原本的数据到字段的映射，原本的数据存储的信息和文件序列都需要存储在数据库中



比如hdfs中存了一个文本（里面有19 male nick），想把这三个字段的值映射到某一个表上，也就是说想用hive去操作这三个字段，在提取字段的时候用这个字段的名称去提取。第一步，把字段和字段名称做唯一映射，映射信息存储在数据库中，当hive以字段名去读取字段的时候，还需要知道字段之间是按什么分隔的。 hive做的事儿就是从mysql中得到字段的映射名称，从hdfs中得到数据信息，然后根据映射字段的信息去读取hdfs中数据信息的内容，hive操作的时候就像是操作数据库一样，然后hive把拿到的数据通过sql语句转化为MapReduce代码，打成jar直接提交到yarn上

理性认识：

1. hive的特性

   操作接口是采用sql语法、HQL

   避免了写MapReduce的繁琐过程

   hive主要是操作MapReduce（hadoop） 所以主要是应用于离线操作

2. hive的体系

   1. client

      1. 终端命令行
      2. jdbc 不常用

   2. metastore

      原本的数据集和字段名称以及数据信息的唯一映射关系

      目前是存储在mysql中

   3. Server-Hadoop

      在操作hive的时候，需要将hadoop的hdfs开启、yarn开启、mapred配置好

3. hive的安装

   1. 解压hive

   2. 改名在cong文件夹 

       mv hive-default.xml.template    hive-site.xml

       mv hive-env.sh.template    hive-env.sh

   3. 配置hive-env.sh

      JAVA_HOME=/opt/modules/jdk1.8.0_121

      HADOOP_HOME=/opt/modules/cdh/hadoop-2.5.0-cdh5.3.6/export 

      HIVE_CONF_DIR=/opt/modules/cdh/hive-0.13.1-cdh5.3.6/conf

   4. 安装Mysql

      ```
      .# yum -y install mysql mysql-server mysql-devel
      .# wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
      .# rpm -ivh mysql-community-release-el7-5.noarch.rpm
      .# yum -y install mysql-community-server  
      
      ```




# hive操作（和mysql基本相似）

show databases;  查看数据库

create database staff;创建一个staff数据库

use staff; 进入staff数据库

show tables; 显示表

在hive建表需要提供字段和字段之间是以什么分割的

创建表 create table t1(eid int,name string,sex string) row format delimited fields terminated by '\t';

查看表的信息 desc formatted t1;

往表中插入信息：

1. 本地导入：load data local inpath '/opt/software/tb.txt' into table staff.t;
2. hdfs导入 不加上面的local 

metastore对于hive中的地位等同于hdfs中的NameNode，所以要及时备份，hive在工作的时候必须连接metastore



hive想操作hdfs中的数据，首先要去metastore中找字段之间的映射关系和文件于文件地址的唯一映射关系（这个意思就是hdfs的文件在哪一个绝对路径上，是在metastore中保存的）

### 备份metastore

备份的基本语法：
				$ mysqldump -uroot -p metastore > metastore.sql
			还原的基本语法：
				$ mysql -uroot -p metastore < metastore.sql

	常见的任务调度框架，可以周期性的执行任务 1和2是流式的任务框架，比如指定任务1完成后跳转到任务3之类，
				1.oozie
				2.azakban
				3.crontab
		这个可以在外面执行hive里面的操作
				hive -e ""
				例子：bin/hive -e "select * from staff.t1;"原理还是启动了hive把名字带进去
				
				hive -f 文件.hql

问题： 在hive里创建了一张表，在mysql中找不到

hive创建的东西会在hdfs中生成/user/hive/werehouse/xxx.db文件，这个.db不是个数据库，hive在体现的形式上和数据库差不多，但实际不是。mysql中metestore中会创建一个唯一映射字段，hive里面是不存东西的，索引信息在mysql中的metestore中，hive拿到这些信息之后才能对hdfs上的/user/hive/werehouse/xxx.db进行操作

### hive的基本流程

![1555395085081](C:\Users\32692\Documents\liunx命令\pic\1555395085081.png)



### 查看历史操作“

cat ~/.hivehistory

### hive的内部表与外部表

默认情况：inner
				hive> CREATE INNER TABLE（报错）
显示指定：external
				hive> CREATE EXTERNAL TABLE

内部表外部表区别：

主要是管理权限不同

	内部表：
				删除表数据时，连同数据源以及元数据信息同时删除
	外部表：
				1、只会删除元数据信息，依旧还有数据源。
				2、共享数据，外部表相对而言也更加方便和安全。
hive在集群内部对数据迁移做的是类似于剪切的工作。

![1555395991318](C:\Users\32692\Documents\liunx命令\pic\1555395991318.png)

本地加载，load data local做的是先将数据put到hdfs，然后在做一个映射关系

### hiveserver2

远程模式，需要修改下配置信息。

<https://blog.csdn.net/leanaoo/article/details/83351240> 

### Sqoop（sql-to-hadoop）

就是工具箱，按照某个格式导数据，依赖于zookeeper

可以从hdfs导到mysql

也可以从mysql导入file中

1. 配置

   开启zookeeper

   开启集群

# 操作阶段

## hive日志清洗操作

需求：按照省份统计pv和uv

## hive制动化处理日志

写shell脚本

## MapReduce数据处理

