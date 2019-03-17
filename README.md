# 常见目录

/dev：Device(设备)的缩写，该目录下存放的是Linux的外部设备，在Linux中访问设备的方式和访问文件的方式是相同的。

/etc：所有的系统管理所需要的配置文件和子目录。

/home：存放普通用户的主目录，在Linux中每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。

/mnt：系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。

/opt：这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。

/root：该目录为系统管理员，也称作超级权限者的用户主目录。

/tmp：这个目录是用来存放一些临时文件的。

/usr： 这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似与windows下的program files目录。

/var：这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。



# 常用快捷键

1. cd +文件夹名 ：进入文件夹
2.  ctrl + c：停止进程
3.  ctrl+l：清屏
4.  ctrl + q：退出
5.  tab：快速补全文件名称
6.  上下键：查找执行过的命令



# 常用编辑操作命令集合

1.  yy 复制当前光标所在的一段   y+数字+y 复制当前光标的下几行

2.  p粘贴  u撤销  dd删除 d+数字+d删除光标下几行

3.  x删除       shift+^ 移动到行头   shift+$  移动到行尾

4.  编辑 ：vi+文件名进入编辑模式 i在插入在光标下一行 a在光标后 o在光标前

5.  查找 ：vi+文件名 进入后 /+要查找的文件名   n下一个  shift+n上一个

   

# 常用文件操作命令集合

默认已进入文件夹情况下进行的操作

1.  pwd ：查看当前所在路径

2. ls 当前目录下文件  ll当前目录下文件详细信息(权限啥的)

3. mkdir +名字： 创建目录   rm -rf +名字 ：删除目录

4. touch+名字 创建文件  rm +名字 ：删除文件

5. cp +文件路径 +要存放的文件夹路径 ：复制文件到某个文件夹

6. cp -r +文件夹路径+要存放的文件夹路径 ：复制文件夹到某个文件夹

7. mv +现在的名字 + 新名字 ： 文件或文件夹重命名

8. mv +文件或文件夹路径+要存放的文件路径 ：移动文件

9. cat + 文件路径 ：查看文件

10.  echo "内容" >>文件 ：将内容追加到文件的末尾 （echo "123" >> test.txt）

11. echo 

    



# root用户管理常用命令集合

1.  useradd ：添加用户
2. passwd +用户名 ：设置用户名密码
3. su +用户名 ：切换用户
4. userdel +用户名：删除用户名
5. userdel + r +用户名：删除用户名相关的所有信息
6. usermod +g + 用户组+用户名 ：将用户名加入到用户组下
7. id + 用户名：查询用户是否建立
8. （groupadd、 groupdel ）+名字 ： 添加或修改组
9.  groupmod -n 新组名 老组名 ：修改组名
10.  cat  /etc/group ：查看创建了哪些组
11. chmod +要修改的权限+ 文件名 ：修改文件或文件夹权限
12. chown + 要给的用户 +文件名：改变用户的所以者
13. chgrp + 要给的组+ 文件名 ：改变用户的组





# 网络设置命令操作

1.  查看当前网络设置：ifconfig
2.  查看网卡信息：vim /etc/udev/rules.d/70-persistent-net.rules（很关键）
3.  ip设置：vim /etc/sysconfig/network-scripts/ifcfg-eth0

​         打开后需设置：以配置完能上网为标准

1. ​        IPADDR=
2. ​        GATEWAY=
3. ​        ONBOOT=yes
4. ​       BOOTPROTO=static
5. ​       DNS1=
6. ​       运行 service network restart

完成网络配置信息



# 配置主机信息操作

1.  查看当前主机名：hostname
2.  修改主机名字：vim /etc/sysconfig/network
3. 修改host文件(方便后期管理，使主机名和ip地址对应) ：vim /etc/hosts
4. sync  将数据由内存同步到硬盘 
5. 重启 reboot



# 打包压缩

1.  压缩：tar -zcvf  XXX.tar.gz   n1.txt    n2.txt   将n1和n2压缩成名字为XXX压缩文件
2.  解压：tar -zxvf  XXX.tar.gz -C+ 解压目的地



# 克隆虚拟机

1.  查看网卡信息，删除原有的eth0 将eth1改为eth0 同时复试网卡的物理地址

    vi /etc/udev/rules.d/70-persistent-net.rules 

2. 修改网络配置信息两处：ip和网卡物理地址

   vi /etc/sysconfig/network-scripts/ifcfg-eth0

3. 修改主机名称

   vi /etc/sysconfig/networw

4. 重启系统

   reboot

5. 开机查看ip 和 ping 主机测试网络连通情况

   

# JDK配置

1. 查看系统原来版本下是否存在JDK版本

   直接输入java 或 rpm -qa |grep java

   

2. 将文件传入linux系统

3. 将Jdk解压缩的某个文件夹

   tar -zxvf hadoop-2.7.2.tar.gz  -C /opt/moudule/

4. 和windows一样，需要配置环境变量

   ]# vi /etc/profile

5. 按住shift+g进入到最后一行

   export#JAVA_HOME=/opt/moudule/jdk1.7.0_79
   export PATH=$PATH:$JAVA_HOME/bin

6. 更新目录文件

   source /etc/profile

7. 输入java 测试配置结果

   

# Hadoop环境变量配置

1. 传入系统+文件解压缩

2. 进入profile文件

   ]# vi /etc/profile

3. 按住shift+g进入到最后一行

   export HADOOP_HOME=/opt/moudule/hadoop-2.7.2
   export PATH=$PATH:$HADOOP_HOME/bin
   export PATH=$PATH:$HADOOP_HOME/sbin

4. source /etc/profile 更新目录文件

5. 为了防止远程找不到文件 所以需要配置Hadoop配置文件中的javaHome 更新为当前javaHome

   vi hadoop-env.sh 



# 本地运行运行Hadoop案例

1. 本地运行grep案例，从一堆配置文件中找到想要的词 

   ​        hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar grep  input output1  'dfs[a-z.]+'

   	grep 表示这个案例
   	
   	input表示从这个文件夹找
   	
   	output表示输出到这个文件夹
   	
   	‘dfs[a-z.]+表示在这一堆文件中找到dfs打头的词

2. 从本地执行一个worldcount案例，统计文件中单词出现的次数

   ​	hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount wcinput/ wcoutput

   

   wordcount ：用这个案例

   wcinput：统计这个文件夹下的单词

   woutput：统计完保存在这个文件夹



# 在HDFS上运行MapReduce案例

1. 指定HDFS中NameNode的地址 在core-site.xml配置

   在configuration中添加配置信息

    <property>
           <name>fs.defaultFS</name>
       <value>hdfs://hadoop09:8020</value>
   </property>

2. 配置：hdfs-site.xml  配置副本数。为了安全起见，在1号机运行之后再配置的机器中的备份

   <!-- 指定HDFS副本的数量 -->

   ​	<property>

   ​		<name>dfs.replication</name>

   ​		<value>1</value>

   ​	</property>

3. 以上信息配置完之后启动集群

   1. 格式化NameNode     在Hadoop目录下 bin/hdfs namenode -format
   2. 启动NameNode   sbin/hadoop-daemon.sh start namenode  
   3. 启动DataNode     sbin/hadoop-daemon.sh start datanode

4. 查看启动信息  #jps

5. 通过Hadoop目录下log日志查看

6. web端查看HDFS文件系统  http://192.168.1.109:50070

7. 在HDFS文件系统上创建一个input文件 

   1. 在Hadoop目录下创建一个多级目录 ： bin/hdfs dfs -mkdir -p /user/zdf/input
   2. hadoop fs -mkdir -p /user/zdf/input1也可以 
   3.  在配置好HADOOP_HOME后 1和2是等价的

8. 将测试文件内容上传到HDFS文件系统的input文件中

   hadoop fs -put wcinput/wc.input /user/zdf/input

9. 在HDFS上运行MapReduce程序

      hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.2.jar wordcount /user/zdf/input /user/zdf/output

10. 查看运行完的文件

    hadoop fs -cat /user/zdf/output/p*

11. 删除上次输出的output结果

    hadoop fs -rmr  hadoop fs -cat /user/zdf/output 

    -rmr 递归删除

    

# 在yarn上运行MapReduce案例

yarn负责资源调度（类似于操作系统）

1.  配置yarn-env.sh

   在Hadoop/etc目录下配置java_home

2. 配置yarn-site.xml

   <property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
   </property>
   <property>
   <name>yarn.resourcemanager.hostname</name>
   <value>hadoop09</value>
   </property>

1. 配置mapred-env.sh

   在Hadoop/etc目录下配置java_home

2. 配置mapred-site-xml-template重新命名为mapred-site.xml

   mapred-site.xml.template mapred-site.xml

   添加配置信息

   <property>

   ​	<name>mapreduce.framework.name</name>

   ​	<value>yarn</value>

   </property>

3. 启动resourcemanger(要首先启动NameNode和DataNode)

   sbin/yarn-daemon.sh start resourcemanager

4. 启动nodemanager(要首先启动NameNode和DataNode)

   sbin/yarn-daemon.sh start nodemanager

5. yarn 的浏览器页面查看

   http://192.168.1.109:8088/cluster

6. 删除output文件

7. 执行MapReduce程序

8. 查看运行结果

   19/03/10 11:59:43 INFO mapreduce.Job:  map 0% reduce 0%
   19/03/10 12:00:13 INFO mapreduce.Job:  map 100% reduce 0%
   19/03/10 12:00:29 INFO mapreduce.Job:  map 100% reduce 100%
   19/03/10 12:00:30 INFO mapreduce.Job: Job job_1552189817456_0001 completed successfully

   map完全执行完之后，才启动reduce

   

   

# 修改本地临时文件存储目录（默认在/tmp目录下）

1.在Hadoop etc目录下 找到core-site.xml 

   	增加配置信息：

​	<property>

​	<name>hadoop.tmp.dir</name>

​	<value>/opt/module/hadoop-2.7.2/data/tmp</value>

​	</property>

2.  退出集群

   namenode和resourcemanager 之后再退datanode和datamanager

   sbin/yarn-daemon.sh stop nodemanager 退出yarn结点管理

   sbin/yarn-daemon.sh stop resourcemanager 退出yarn资源管理

   sbin/hadoop-daemon.sh stop datanode 退出Hadoop结点

   sbin/hadoop-daemon.sh stop namenode 退出Hadoop目录

3. 删除原位置的临时文件存储目录

4. 删除Hadoop目录下log文件夹

5. 格式化集群

   bin/hdfs namenode -format

6. 重启集群即可



# centOS将文件拷贝到CentOS

[root@hadoop09 software]# scp -f hadoop-2.7.2.tar.gz root@hadoop02:/opt/software/





# 配置ssh无密码登录

1. A想免密访问B  A要生成免密公钥对（一个公钥一个私钥） 将A的公钥拷贝到B的authorized_key ，A传送的数据是用私钥A加密，传送到B之后通过公钥A来解密。B的返回信息用A的公钥加密，之后A用自己的私钥解密数据

2. 在命令行输入cd 进入到自己的home目录 输入 ls -al  找到.ssh 进入查看 known_hosts为曾经访问过的服务器

   ​	（1）~/.ssh/known_hosts	：记录ssh访问过计算机的公钥(public key)

   ​	（2）id_rsa	：生成的私钥

   ​	（3）id_rsa.pub	：生成的公钥

   ​	（4）authorized_keys	：存放授权过得无秘登录服务器公钥

3. 操作流程

   1. ssh-keygen -t rsa   在.ssh目录下输入，生成公钥和秘钥

   2. ssh-copy-id 192.168.1.102  将公钥拷贝到目标服务器

      


# rsync远程同步工具

主要用于备份和镜像。具有速度快、避免复制相同内容和支付符号链接的优点

1.  rsync -rvl zdf/  root@hadoop03:/opt/sortware/ 将本机zdf文件夹的内容复制到hadoop03的sortware文件夹下

   

# 完全分布式的搭建

![1552289597072](C:\Users\32692\AppData\Local\Temp\1552289597072.png)



在hadoop102需要配置

1. core-site.xml 中配置namenode和文件存储路径

   <!-- 指定HDFS中NameNode的地址 -->
   	<property>
   		<name>fs.defaultFS</name>
           <value>hdfs://hadoop02:8020</value>
   	</property>
   	<!-- 指定hadoop运行时产生文件的存储目录 -->
   	<property>
   		<name>hadoop.tmp.dir</name>
   		<value>/opt/module/hadoop-2.7.2/data/tmp</value>
   	</property>

2. hadoop-env.sh 中配置JAVA_HOME 

   export  JAVA_HOME=/opt/module/jdk1.7.0_79

3. hdfs-site.xml 中配置副本数和namenode.secondary

   <configuration>	

   ​	<property>

   ​		<name>dfs.replication</name>

   ​		<value>3</value>

   ​	</property>

   ​	<property>

   ​        <name>dfs.namenode.secondary.http-address</name>

   ​        <value>hadoop104:50090</value>

   ​    </property>

   </configuration>

4. slaves配置 数据节点 DataNode有几个放几个

   hadoop02

   hadoop03

   hadoop04

5. 配置yarn-env.sh

   配置 java_home

6. yarn-site  配置nodemanager和resourcemanager

   <!-- Site specific YARN configuration properties -->

   <!-- reducer获取数据的方式 -->

   ​    <property>

   ​        <name>yarn.nodemanager.aux-services</name>

   ​        <value>mapreduce_shuffle</value>

   ​    </property>

   <!-- 指定YARN的ResourceManager的地址 -->

   ​	<property>

   ​		<name>yarn.resourcemanager.hostname</name>

   ​		<value>hadoop103</value>

   ​	</property> 

7. mapred-env.sh 在MapReduce中修改JAVA_HOME

8. mapred-site.xml中指定MapReduce运行在yarn上

   <!-- 指定mr运行在yarn上 -->
   	<property>
   		<name>mapreduce.framework.name</name>
   		<value>yarn</value>
   	</property>

9. 将以上配置同步至所有的服务器

10. 启动集群 

   1.  bin/hdfs namenode -format, 格式化namenode
   2.  sbin/start-dfs.sh  启动hdfs
   3.  sbin/start-yarn.sh 启动yarn
   4.  在每个服务器查看启动情况



# 集群操作文件上传下载

上传 查看 删除

1. 集群上传的文件都按块存储在core-site.xml配置的存储目录下

2. 查看多块文件时，新建一个文件夹利用重定向技术拼接存储块

   操作过程：

   1. 进入到存储块的目录下 

      /opt/module/hadoop-2.7.2/data/tmp/dfs/data/current/BP-368187420-192.168.1.102-1552303207579/current/finalized/subdir0/subdir0

   2. 利用重定向拼接

      [root@hadoop02 subdir0]# cat blk_1073741825 >> temp 
      [root@hadoop02 subdir0]# cat blk_1073741826 >> temp 

   3. 查看文件

   4. 下载文件 

   

# 集群的启动方式（三种）

1. 单独启动   （服役新节点的时候用）

   hadoop-daemon.sh  start|stop  namenode|datanode|secondarynamenode

   yarn-daemon.sh  start|stop  resourcemanager|nodemanager

2. 整体启动dfs或yarn（最常用）

   start-dfs.sh

   start-yarn.sh

3. 全部启动 ：start-all.sh （非常不建议使用）

4. 

# HDFS概念和组成

# 自定义机架感知

1.创建类实现DNSToSwitchMapping接口， 在eclipse中创建项目

# 一致性模型

​    在客户端数据上传到集群中时，如上传的是的DataNode1结点且上传成功， 如果后来两个结点的数据还没有变，此时再来一个客户端直接读的是DataNode3的数据，这样话读取诗句就不一致了。

​    这时候就需要一致性模型，在写入时进行同步刷新，加上fos.hflush（），这样使数据及时刷新保持同步、但是需要底层同步完毕之后才能读取



# NameNode和SecondaryNode工作机制

NameNode：NameNode启动之后首先加载编辑日志和镜像文件到内存，当客户端发送元数据的增删改请求时，NameNode记录操作日志，更新滚动日志，然后在内存中进行操作。

SecondaryNode：辅助namenode工作，1.首先请求是否需要checkpoint（就是NameNode的edit和fsimage是否需要和并）checkpoint的触发条件（1.定时时间到 2.edits中数据满了）2.请求执行checkpoint，NameNode滚动正在写的edits，NameNode把正在写的edits.inprogress转变为edits003（假设已经有edit002存在），同时再生成一个新的edits.inprogerss,记录后续操作，SecondaryNode拿过edit02和edit03还有原始的fsimage加载到内存中合并 3. 在SecondaryNode生成新的fsimage，在回送到namenode中，去替换namenode中的原始fsimage。SecondaryNode帮助NameNode合并加载日志和镜像文件、减少NameNode的工作量，这两个结点都非常耗内存，所以不放在一个服务器上。



# 编辑日志和镜像文件

进入 /opt/module/hadoop-2.7.2/data/tmp/dfs  会有当前服务器配置的结点信息





1.  首先进入./namenode  有 in_use.lock，这个是namenode故障的时候，文件夹不能任意移动。

2. 进入./namenode/current 有日志和镜像文件

   -rw-r--r--. 1 root root      42 3月  14 12:11 edits_0000000000000000001-0000000000000000002
   -rw-r--r--. 1 root root      42 3月  14 13:11 edits_0000000000000000003-0000000000000000004
   -rw-r--r--. 1 root root      42 3月  14 14:11 edits_0000000000000000005-0000000000000000006
   -rw-r--r--. 1 root root      42 3月  14 15:11 edits_0000000000000000007-0000000000000000008
   -rw-r--r--. 1 root root      42 3月  14 16:12 edits_0000000000000000009-0000000000000000010
   -rw-r--r--. 1 root root      42 3月  14 17:12 edits_0000000000000000011-0000000000000000012
   -rw-r--r--. 1 root root 1048576 3月  14 17:12 edits_inprogress_0000000000000000013
   -rw-r--r--. 1 root root     350 3月  14 16:12 fsimage_0000000000000000010
   -rw-r--r--. 1 root root      62 3月  14 16:12 fsimage_0000000000000000010.md5
   -rw-r--r--. 1 root root     350 3月  14 17:12 fsimage_0000000000000000012
   -rw-r--r--. 1 root root      62 3月  14 17:12 fsimage_0000000000000000012.md5
   -rw-r--r--. 1 root root       3 3月  14 17:12 seen_txid  //最新编辑的版本号
   -rw-r--r--. 1 root root     204 3月  14 12:09 VERSION

3. fsimage文件 ：hdfs文件系统元数据的一个永久性检查点，其中包含hdfs文件系统的所有目录文件和文件idnode的序列化信息

4. edits文件：存放hdfs文件系统的所有更新操作的路径，文件系统客户端所有执行的写操作都会被记录到edits中

5. 每次NameNode启动额时候都会讲fsimage文件读入到内存中并从最小的edit00到seen_txid记录的数据执行更新操作，保证操作内存中的元数据是最新的。也就是说，在NameNode启动时，首先将NameNode和fsimage进行了合并

6. 对NameNode进行format操作之后，就会产生edits fsimage seen_txid   VERSION

7. 

查看镜像文件命令 ：# hdfs oiv -p XML  -i fsimage_0000000000000000010 -o ./fsimage.xml

fsimage中存放：hadoop上传的文件夹信息 权限 类型 id 名字 副本数啊之类的

	<INodeSection>
		<lastInodeId>16385</lastInodeId>
		<inode>
			<id>16385</id>
			<type>DIRECTORY</type>
			<name></name>
			<mtime>0</mtime>
			<permission>root:supergroup:rwxr-xr-x</permission>
			<nsquota>9223372036854775807</nsquota>
			<dsquota>-1</dsquota>
		</inode>
	</INodeSection>
edit中记录操作日志：# hdfs oev -p XML -i edits_0000000000000000013-0000000000000000014 -o ./edit.xml

<EDITS>
  <EDITS_VERSION>-63</EDITS_VERSION>
  <RECORD>
    <OPCODE>OP_START_LOG_SEGMENT</OPCODE>
    <DATA>
      <TXID>13</TXID>
    </DATA>
  </RECORD>
  <RECORD>
    <OPCODE>OP_END_LOG_SEGMENT</OPCODE>
    <DATA>
      <TXID>14</TXID>
    </DATA>
  </RECORD>
</EDITS>



# 滚动日志

命令 ： hdfs dfsadmin -rollEdits

最初的fsimage是在namenode格式化的时候



# secondarynode和NameNode的current目录结构基本相同（少了一个seed文件）

好处： 安全性 如果namenode发生故障没有及时备份，可以从secondarynode中获取备份或者直接将secondarynode变为主目录

恢复数据的方法：

1.  从secondarynode中获取备份，拷贝到NameNode目录下
2. 使用-importCheckpoint选项启动namenode守护进程，从而将secondarynode变为新的NameNode

# 集群的安全模式

Namenode启动时，首先将映像文件（fsimage）载入内存，并执行编辑日志（edits）中的各项操作。一旦在内存中成功建立文件系统元数据的映像，则创建一个新的fsimage文件和一个空的编辑日志。此时，namenode开始监听datanode请求。但是此刻，namenode运行在安全模式，即namenode的文件系统对于客户端来说是只读的。

系统中的数据块的位置并不是由namenode维护的，而是以块列表的形式存储在datanode中。在系统的正常操作期间，namenode会在内存中保留所有块位置的映射信息。在安全模式下，各个datanode会向namenode发送最新的块列表信息，namenode了解到足够多的块位置信息之后，即可高效运行文件系统。
	
如果满足“最小复本条件”，namenode会在30秒钟之后就退出安全模式。所谓的最小复本条件指的是在整个文件系统中99.9%的块满足最小复本级别（默认值：dfs.replication.min=1）。在启动一个刚刚格式化的HDFS集群时，因为系统中还没有任何块，所以namenode不会进入安全模式。

集群处于安全模式，不能执行重要操作（写操作）。集群启动完成后，自动退出安全模式。



安全模式的使用场景：系统维护升级的时候，大盘点的时候



# 服役新结点

1. 准备一台新机器（克隆）

2. 在namenode的/opt/module/hadoop-2.7.2/etc/hadoop目录下创建dfs.hosts文件(NameNode结点主机下)

   将要添加的结点加入其中

3. 在hdfs-site.xml下添加（dfs.host列出了连入namenode的节点 ，为空的话任何结点都可）

   ```
       <property>
       <name>dfs.hosts</name>
     	<value>/opt/module/hadoop-2.7.2/etc/hadoop/dfs.hosts</value>
       </property>
   ```

4. 刷新NameNode结点 ：hdfs dfsadmin -refreshNodes

5. 刷新yarn ： # yarn rmadmin -refreshNodes

6. 在namenode的slaves文件中增加新服务器名称

7. 在新节点启动datanode和nodemanager

8. 在web端查看即可

9. sbin/start-balancer.sh 这个是数据平衡命令，当某个结点非常满某个非常空，就用这个来平衡

# 退役旧结点（退役的过程中，要把数据复制到别的结点上）

1. 在namenode的/opt/module/hadoop-2.7.2/etc/hadoop目录下创建dfs.hosts.exclude文件(NameNode结点主机下)

   将要退役的结点加入其中

2. 在hdfs-site.xml下添加

   <property>
   	<name>dfs.hosts.exclude</name>
         <value>/opt/module/hadoop-2.7.2/etc/hadoop/dfs.hosts.exclude</value>
   </property>

3. 刷新NameNode结点 ：hdfs dfsadmin -refreshNodes

4. 刷新yarn ： # yarn rmadmin -refreshNodes

5. 通过单命令行的形式停止掉结点

    sbin/hadoop-daemon.sh stop datanode

    sbin/yarn-daemon.sh stop nodemanager# sbin/yarn-daemon.sh stop nodemanager

6. 修改slave文件 等等

# DataNode工作机制

1.  DataNode启动后向NameNode注册、NameNode返回注册成功
2.  DataNode开始之后、每小时向NameNode上报DataNode所有的信息
3.  心跳信息每3秒一次，心跳返回带有NameNode给该DataNode的命令
4.  NameNode 十分钟没有收到DataNode的心跳信息，就默认DataNode挂掉
5.  数据校验和：保证传递的数据错了，能检测到 （如奇偶校验等）

# datanode目录结构

进data/temp/data看看了解，存放实际的上传的内容

# 数据拷贝

1.  两个主机间的数据拷贝 

   1. 	拷贝到03服务器 scp 317day.txt root@hadoop03:/opt/module/
      	317day.txt                                                 100%   11     0.0KB/s   00:00 
      	从03服务器获取文件到本地 scp root@hadoop03:/opt/module/317day-return.txt 317day-03return.txt 
      	

2. 集群间拷贝



# hadoop存档

1. 理论：

    	文件按块存储，每个块的元数据都存在NameNode中，所以hadoop存储小文件效率会很低（因为存储小文件也是按块存储，可能1K的数据独自在128m的块中，但是这不影响别的数据继续存再这个块）

   HAR文件，是一个高效的文件存档文件（作用类似于把小文件打包成一个整体，让NameNode认为这是一个文件，实际还是分着的）目的是介绍NameNode的内存。

2. 启动集群

   命令：hadoop archive -archiveName clear.har -p   /user/zdf   /user

   19/03/17 16:01:52 INFO mapreduce.Job:  map 0% reduce 0%
   19/03/17 16:02:26 INFO mapreduce.Job:  map 100% reduce 0%
   19/03/17 16:02:40 INFO mapreduce.Job:  map 100% reduce 100%

   走的是MapReduce

   存储完编程索引的方式

3. 查看 

   hadoop fs -lsr har:///user/clear.har

# 快照功能

发生活动时保存当下状态（如写入时）

# 回收站

官网有介绍

在core-site.xml里配置