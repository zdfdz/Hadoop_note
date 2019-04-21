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



# MapReduce

​	MapReduce是一个分布式运算程序的编程框架，核心功能是将用户编写的业务逻辑代码和自带的组件整合成分布式运算程序，并发运行在hadoop集群上

​	为什么要用MapReduce

​		1.海量数据在单机上处理因为硬件的闲置

​		2.单机版程序扩展到集群来分布式运行，将极大增加程序的复杂度

​		3.引入MapReduce后，开发人员可以把绝大部分工作集中在业务逻辑开发，而将分布式计算中的复杂性的问题交给框架处理

​		4.MapReduce分布式框架考虑的问题

​			1.逻辑运算要不要先分后合

​			2.程序如何分配运算任务（切片）

​			3.两阶段的程序如何启动？如何协调

 1. map和reduce（三大管理者：maptask、reducetask、MrAppMaster）

    1. map主要处理并行任务，比如切分任务分配
    2. 分布式程序至少分成两个阶段（map切分分配，然后reduce合并）
    3. 第一阶段（map把任务分配到了3个结点）的maptask（读数据、按行处理数据、默认按空格切分、用hashmap存储、等任务都读完之后，分区排序）并发实例互不相干，没有任何交互
    4. 第二阶段的reducetask也是互不相干的，各自统计自己应该统计的逻辑，但是依赖于所有的maptask。
    5. MapReduce模型只包含一个map阶段和reduce阶段，但是可以有多个map串行运行（mapA和mapB串行运行，mapA运行完之后，把结果给mapB，mapB在mapA结果的基础上二次计算）
    6. MrAppMaster负责整个程序的过程调度及状态协调

 2. 序列化概念

    1. 序列化就是把内存中的对象，转化成字节序列（或其他的数据传输协议）以便于存储（持久化）和网络传输
    2. 反序列化就是将收到的字节序列（或其他数据的传输协议）或者是硬盘持久化数据，转化成内存中的对象
    3. java序列化框架Serializable ，一个对象被被序列化之后，会有很多的额外信息（header、校验信息、继承体系等等），不适合在网络中高效传输.优势 安全、体系完整。
    4. hadoop自己的蓄力序列化机制 writable，高效

 3. 常见的序列化类型（Java  And Hadoop）

    1. int  IntWritable

    2. long LongWritable

    3. string Text

    4. Double DoubleWritable 

       

# 并行度决定机制

  maptask的并行度决定map阶段的任务处理并发，并且影响整个job的处理速度。但是maptask并行任务是否越多越好，并行度该如何决定？

1. 一个job的map阶段并行度由客户端在提交job时决定（源码可以看到）
2. 每一个split切片分配一个maptask并行实例处理
3. 默认情况下，切片大小=blocksize

 举例子描述：

​	如果有一个300m大小的文件，会分三个块来存储，第一个块存储128m，第二个块存储128m，第三块存储44m，这样会有三个maptask来处理每个块的数据。

​	如果就一个50m大小的数据，那么一个块足矣存储，只开一个maptask就可以了



# job提交源码分析

# inputFormat源码分析

# Map和reduce数据传输需要序列化

# shuffle机制

map之后 reduce之前，都是shuffle的过程

# MapReduce详细工作流程



# 在reduce端和并数据

# 在map端合并数据

理由：为了避免数据倾斜（map端将数据处理之后，提交到reduce端，reduce又需要大量和并工作，处理起来非常困难）、可以选择在map端和并数据。



# 小文件处理（自定义InputFormat）

无论hdfs还是MapReduce对小文件都有损耗



# 基础知识整理：

​	hadoop组成：HDFS yarn MapReduce

## 	HDFS 

​	是一个文件系统，通过目录树来定位文件。是分布式架构。文件不支持修改，适合一次写入大量读出的场景应用。

组成：HDFS集群包括，NameNode和DataNode以及Secondary Namenode。

1.  NameNode：负责管理整个文件系统的元数据，以及每一个路径（文件）所对应的数据块信息。
2. DataNode：实际的存储位置
3. Secondary Namenode：用来监控HDFS状态的辅助后台程序，每隔一段时间获取HDFS元数据的快照。

写入流程理解：

![1553485448371](C:\Users\32692\AppData\Local\Temp\1553485448371.png)

  其实不难理解，上数据会向NameNode发请求，之后客户端等NameNode返回的信息，如果可以上传，就继续想NameNode请求可上传的DataNode，客户端和DataNode去建立传输通道，之后就可以传输数据了。当第一个block传输完之后，客户端再次请求namenode第二个block放在那个DataNode



4. 文件块：128Mb  理论依据寻址时间为传输速率的1%，现在磁盘大概是100m/s,所以块大小为128mb刚刚好。当然，块的大小可以（dfs.blocksize）

5. 命令执行： hadoop fs -巴拉巴拉（只对于文件操作，hdfs是文件操作系统嘛）

6. 机架感知

7. Hadoop2.7.2副本节点选择

   ​	第一个副本在client所处的节点上。如果客户端在集群外，随机选一个。

   ​	第二个副本和第一个副本位于相同机架，随机节点。

   ​	第三个副本位于不同机架，随机节点。

hdfs读取流程理解：

![1553494648345](C:\Users\32692\AppData\Local\Temp\1553494648345.png)



8. 一致性模型：在客户端数据上传到集群中时，如上传的是的DataNode1结点且上传成功， 如果后来两个结点的数据还没有变，此时再来一个客户端直接读的是DataNode3的数据，这样话读取诗句就不一致了。

   ​    这时候就需要一致性模型，在写入时进行同步刷新，加上fos.hflush（），这样使数据及时刷新保持同步、但是需要底层同步完毕之后才能读取

9. NameNode和Secondary namenode工作机制

   edit可以去操作fsimage，当用户发出一条指令之后（修改操作才会记录），会首先写入edit中。客户端发生修改fsimage的操作，NameNode会首先滚动日志，产生新的edits记录，另外配合一个edits.impress（这个记录当前操作）

   Secondary namenode帮助NameNode将edits和fsimage合在一起将最新的fsimage给NameNode。（hdfs dfsadmin -rollEdits 这个命令强制回滚日志）

   ![1553496993841](C:\Users\32692\AppData\Local\Temp\1553496993841.png)

   10. Secondary NameNode用来监控HDFS状态的辅助后台程序，每隔一段时间获取HDFS元数据的快照。

   11. 集群安全模式：这个是当NameNode刚刚启动的时候，需要namenode开始监听datanode请求。但是此刻，namenode运行在安全模式，即namenode的文件系统对于客户端来说是只读的。

       数据块的位置并不是由namenode维护的，而是以块列表的形式存储在datanode中。在系统的正常操作期间，namenode会在内存中保留所有块位置的映射信息。在安全模式下，各个datanode会向namenode发送最新的块列表信息，namenode了解到足够多的块位置信息之后，即可高效运行文件系统。（简单来说可以理解为当DataNode和NameNode需要大量信息交互的时候需要集群的安全模式）

   12. DataNode工作机制

       ![1553571573759](C:\Users\32692\AppData\Local\Temp\1553571573759.png)

   13. 新节点的服役

       在namenode的/opt/module/hadoop-2.7.2/etc/hadoop目录下创建dfs.hosts文件

       在namenode的hdfs-site.xml配置文件中增加dfs.hosts属性

       刷新NameNode ： hdfs dfsadmin -refreshNodes

       更新resourcemanager节点

       在namenode的slaves文件中增加新主机名称

       单命令启动

       实现数据平衡sbin/start-balancer.sh

   14. 退役结点

       在namenode的/opt/module/hadoop-2.7.2/etc/hadoop目录下创建dfs.hosts.exclude文件

       在namenode的hdfs-site.xml配置文件中增加dfs.hosts.exclude属性

       刷新namenode、刷新resourcemanager

       检查web浏览器，退役节点的状态为decommission in progress（退役中），说明数据节点正在复制块到其他节点。

       从namenode的dfs.hosts文件中删除退役节点

       刷新namenode，刷新resourcemanager

       slave文件中删除退役节点

       实现数据平衡sbin/start-balancer.sh

   15. 远程文件拷贝 scp

       scp -r abc.txt root@zdf01:/opt/abc.txt //当前服务器传到另一个服务器

       scp -r  root@zdf01:/opt/abc.txt  /opt/abc.txt //当前zdf01服务器下载abc文件到本地

   16. **rsync  主要用于备份和镜像。具有速度快、避免复制相同内容和支付符号链接的优点**（很长用）

       1. rsync -rvl zdf/  root@hadoop03:/opt/sortware/ 将本机zdf文件夹的内容复制到hadoop03的sortware文件夹下

## MapReduce

1. 概念：Mapreduce是一个分布式运算程序的编程框架，是用户开发“基于hadoop的数据分析应用”的核心框架；Mapreduce核心功能是将用户编写的业务逻辑代码和自带默认组件整合成一个完整的分布式运算程序，并发运行在一个hadoop集群上。引入mapreduce框架后，开发人员可以将绝大部分工作集中在业务逻辑的开发上，而将分布式计算中的复杂性交由框架来处理。

2. MapReduce分为两个阶段：一个是map阶段（切分数据）、一个是reduce阶段（合并数据）

   map阶段主要实现并行任务，可以理解为把数据切分成一块一块的那种

   分布式的运算程序往往需要分成至少2个阶段

3. mapTask进程完成具体的切分任务

   第一个阶段的maptask并发实例，完全并行运行，互不相干

   1. 一行一行的读数据
   2. 按要求切分读进来的数据
   3. 按要求返回当前统计的值（不合并，如统计某个单词出现的次数：zdf，1；zdf，1，只做统计不合并）
   4. 等到分给自己的数据片全部读取完毕之后
   5. 进行分区排序

4. reduce阶段

   1. 第二个阶段的reduce task并发实例互不相干，但是他们的数据依赖于上一个阶段的所有maptask并发实例的输出
   2. reduce阶段负责统计map的切分的结果
   3. MapReduce编程模型只能包含一个map阶段和一个reduce阶段，如果用户的业务逻辑非常复杂，那就只能多个mapreduce程序，串行运行（但是多个map阶段可以多个map串行工作）

5. 思考问题

   1. maptask如何分配？
   2. reducetask是如何分配？
   3. map阶段和reduce阶段的衔接问题？

6. MrAppMaster负责整个程序的过程调度及状态协调

7. 一个完整的mapreduce程序在分布式运行时有三类实例进程：

   1）MrAppMaster：负责整个程序的过程调度及状态协调

   2）MapTask：负责map阶段的整个数据处理流程

   3）ReduceTask：负责reduce阶段的整个数据处理流程

8. MapReduce编程规范

   用户编写的程序分成三个部分 mapper reduce Driver三个阶段

   1. Mapper阶段

      读入数据（通过inputformat以键值对的形式读取数据），行号为K每行内容为V，map方法对每一个<k,v>都调用一次

      输出也是自定义Kv形式（只输出，不合并）

      map方法是输出到缓存区（写入outputCollector中，在这里面进行分区排序巴拉巴拉，这里面开几个分区就决定了开几个reduce）中，并不是直接给reduce

      当缓存区使用的内存达到80%的时候，就写出去

   2. reduce阶段

      输入是mapper的输出类型

      reduceTask进程把对每一组相同K的<k，v>组调用一次reduce方法

   3. Driver阶段

      整个程序需要一个Driver来进行提交，提交的是一个描述了各种必要信息的Job对象。

   ## MapReduce运行流程

    ![img](file:///C:\Users\32692\AppData\Local\Temp\ksohtml25584\wps1.png)

   1）在MapReduce程序读取文件的输入目录上存放相应的文件。

   2）客户端程序在submit()方法执行前，获取待处理的数据信息，然后根据集群中参数的配置形成一个任务分配规划。

   3）客户端提交job.split、jar包、job.xml等文件给yarn，yarn中的resourcemanager启动MRAppMaster。

   4）MRAppMaster启动后根据本次job的描述信息，计算出需要的maptask实例数量，然后向集群申请机器启动相应数量的maptask进程。

   5）maptask利用客户指定的inputformat来读取数据，形成输入KV对。

   6）maptask将输入KV对传递给客户定义的map()方法，做逻辑运算

   7）map()运算完毕后将KV对收集到maptask缓存。

   8）maptask缓存中的KV对按照K分区排序后不断写到磁盘文件

   9）MRAppMaster监控到所有maptask进程任务完成之后，会根据客户指定的参数启动相应数量的reducetask进程，并告知reducetask进程要处理的数据分区。

   10）Reducetask进程启动之后，根据MRAppMaster告知的待处理数据所在位置，从若干台maptask运行所在机器上获取到若干个maptask输出结果文件，并在本地进行重新归并排序，然后按照相同key的KV为一个组，调用客户定义的reduce()方法进行逻辑运算。

   11）Reducetask运算完毕后，调用客户指定的outputformat将结果数据输出到外部存储。

   补充：outputCollector决定了reduce中分区的个数，map阶段读数据使用inputFormat框架输出时并不是直接输出给reduce，而是输出在outputCollector中进行分区排序后写入磁盘（目的就是决定reduce的分区的个数）、reduce阶段的写出使用outputFormat框架

### 序列化

序列化就是把内存中的对象，转化为字节序列以便于存储（持久化）和网络传输（map中和reduce中传递的信息都是序列化过的）

反序列化就是将收到的字节序列或者硬盘持久化数据，转化为内存中的对象

java序列化是一个重量级序列化框架serializable ，一个对象被序列化会带有很多额外的信息（各种校验信息、header、继承体系等等）

### 自定义bean对象

1）自定义bean对象要想序列化传输，必须实现序列化接口，需要注意以下7项。

（1）必须实现Writable接口

（2）反序列化时，需要反射调用空参构造函数，所以必须有空参构造

（3）重写序列化方法

（4）重写反序列化方法

（5）注意反序列化的顺序和序列化的顺序完全一致

（6）要想把结果显示在文件中，需要重写toString()，且用”\t”分开，方便后续用

（7）如果需要将自定义的bean放在key中传输，则还需要实现comparable接口，因为mapreduce框中的shuffle过程一定会对key进行排序

### mapTask并行度决定机制

maptask的并行度决定map阶段的任务处理并发度，进而影响整个job的处理速度，那么并行度是如何决定的呢？

并行度的意思就是maptask同时启动几个

job的map阶段的并行度是由客户端提交job的时候决定

job的划分的任务的split切片分配一个mapTask并行实例处理

默认情况下，切片大小=blocksize



### job提交流程（客户端提交的流程）

这个过程完成了建立连接、判断远程还是本地yarn，提交完成了获取路径和计算切片信息，生成切片规划文件（由input.getSplit（job）完成）、然后提交job返回提交状态

#### FileInputFormat源码解析(input.getSplits(job))

（1）找到你数据存储的目录。

​	（2）开始遍历处理（规划切片）目录下的每一个文件

​	（3）遍历第一个文件ss.txt

​		a）获取文件大小fs.sizeOf(ss.txt);

​		b）计算切片大小computeSliteSize(Math.max(minSize,Math.max(maxSize,blocksize)))=blocksize=128M

c）默认情况下，切片大小=blocksize

​		d）开始切，形成第1个切片：ss.txt—0:128M 第2个切片ss.txt—128:256M 第3个切片ss.txt—256M:300M（每次切片时，都要判断切完剩下的部分是否大于块的1.1倍，不大于1.1倍就划分一块切片）

​		e）将切片信息写到一个切片规划文件中

​		f）整个切片的核心过程在getSplit()方法中完成。

g）<u>数据切片只是在逻辑上对输入数据进行分片，并不会再磁盘上将其切分成分片进行存储</u>。InputSplit只记录了分片的元数据信息，比如起始位置、长度以及所在的节点列表等。

h）注意：block是HDFS上物理上存储的存储的数据，切片是对数据逻辑上的划分。

​	（4）提交切片规划文件到yarn上，yarn上的MrAppMaster就可以根据切片规划文件计算开启maptask个数。

```
// 根据文件类型获取切片信息

FileSplit inputSplit = (FileSplit) context.getInputSplit();

// 获取切片的文件名称

String name = inputSplit.getPath().getName();
```

#### 小文件分片能处理

####  **CombineTextInputFormat****切片机制**

关于大量小文件的优化策略

1）默认情况下TextInputformat对任务的切片机制是按文件规划切片，不管文件多小，都会是一个单独的切片，都会交给一个maptask，这样如果有大量小文件，就会产生大量的maptask，处理效率极其低下。

2）优化策略

​	（1）最好的办法，在数据处理系统的最前端（预处理/采集），将小文件先合并成大文件，再上传到HDFS做后续分析。

​	（2）补救措施：如果已经是大量小文件在HDFS中了，可以使用另一种InputFormat来做切片（CombineTextInputFormat），它的切片逻辑跟TextFileInputFormat不同：它可以将多个小文件从逻辑上规划到一个切片中，这样，多个小文件就可以交给一个maptask。

​	（3）优先满足最小切片大小，不超过最大切片大小

​		CombineTextInputFormat.*setMaxInputSplitSize*(job, 4194304);// 4m

​		CombineTextInputFormat.*setMinInputSplitSize*(job, 2097152);// 2m

​	举例：0.5m+1m+0.3m+5m=2m + 4.8m=2m + 4m + 0.8m

3）具体实现步骤

```
// 如果不设置InputFormat,它默认用的是TextInputFormat.class
job.setInputFormatClass(CombineTextInputFormat.class)
CombineTextInputFormat.setMaxInputSplitSize(job, 4194304);// 4m
CombineTextInputFormat.setMinInputSplitSize(job, 2097152);// 2m
```

#### shuffle MapReduce中对数据处理最核心的框架

概述：

mapreduce中，map阶段处理的数据如何传递给reduce阶段，是MapReduce中最关键的一个流程，这个流程就是shuffle；

shuffle：洗牌、发牌（核心机制：数据分析、排序、缓存）

具体来说：就是将maptask输出的处理结果数据，分发给reducetask，并在分发的过程中，按照<u>Key进行了分区和排序</u>![1553826032242](C:\Users\32692\AppData\Local\Temp\1553826032242.png)

shuffle 针对Key值进行排序

partition分区

bean继承WritableComparable实现排序

writeable序列化接口打通了map和reduce传输的通道

#### combine

combine在是合并每个maptask中的数据，然后再给reduce合并全部的数据，这样提高了效率，它的父类就是reducer，运行在maptask的节点上，combine应用的前提是不能影响最终的业务逻辑

#### groupingComparator 分组

在reduce阶段对数据举行合并



## yarn

概念：yarn是一个资源调度平台，负责为运算程序提供服务器运算资源，相当于一个分布式的操作系统，而MapReduce等运算程序相当于运行在操作系统之上的应用程序 

#### 	重点

​	1）Yarn并不清楚用户提交的程序的运行机制

​	2）Yarn只提供运算资源的调度（用户程序向Yarn申请资源，Yarn就负责分配资源）

​	3）Yarn中的主管角色叫ResourceManager

​	4）Yarn中具体提供运算资源的角色叫NodeManager

​	5）这样一来，Yarn其实就与运行的用户程序完全解耦，就意味着Yarn上可以运行各种类型的分布式运算程序（mapreduce只是其中的一种），比如mapreduce、storm程序，spark程序……

​	6）所以，spark、storm等运算框架都可以整合在Yarn上运行，只要他们各自的框架中有符合Yarn规范的资源请求机制即可

​	7）Yarn就成为一个通用的资源调度平台，从此，企业中以前存在的各种运算集群都可以整合在一个物理集群上，提高资源利用率，方便数据共享

#### 	yarn工作机制

   	1.  客户端向resourcemanager申请一个application
  2.  resourcemanager返回一个application资源提交的路径 hdfs://..../.staging以及application_id
  3.  客户端提交资源（job.submit()后生成 Job.split、job.xml、wc.jar）
  4.  资源提交完成，申请运行MrAppmaster（此时和客户端就没什么关系了）
  5.  在resourcemanager中，用户的请求初始化成一个task（资源调度要根据优先级去执行），放到任务的任务的调度队列
  6.  NodeManager到任务中领取任务，并在创建一个container（里面包括cpu+ram和MrAppmaster）
  7.  从集群中读取数据（切片信息）到自己的container中
  8.  由MrAppmaster根据Job.Split向resourcemanager申请maptask
  9.  resourcemanager返回分配的nodeManger（也有一个container，也是包含cpu+ram+jar），有Mrappmaster调遣，发送程序启动脚本
  10.  MrAppMaster向Rm申请reduce容器（数量根据要求来），有Rm返回reduce资源
  11.  reduce向map获取相应的分区数据，开始根据Key值合并处理
  12.  程序运行结束之后。Mr向Rm注销自己，回收资源

# Zookeeper

Zookeeper从设计模式角度来理解：是一个基于观察者模式设计的分布式服务管理框架，**它负责存储和管理大家都关心的数据**，然后接受观察者的注册，一旦这些数据的状态发生变化，Zookeeper就将负责通知已经在Zookeeper上注册的那些观察者做出相应的反应，从而实现集群中类似Master/Slave管理模式

Zookeeper=文件系统+通知机制

Zookeeper一般存储小的管理配置文件

通知机制：就是zookeeper文件系统上存储文件发生改变就是进行通知

## 应用场景

提供的服务包括 分布式消息同步和协调机制、服务器节点动态上下线、统一配置管理、负责均衡、集群管理

数据信息的发布

![1554168098060](C:\Users\32692\AppData\Local\Temp\1554168098060.png)

软负载均衡

![1554168461800](C:\Users\32692\AppData\Local\Temp\1554168461800.png)

## zookeeper安装：

1. 解压jdk到目录

2. 创建一个放置存放文件的目录

3. 进入zookeeper --->conf --->zoo.cfg（先把名字改成这个） 配置一下dataDir，将第2步路径换上去（配置了方便点，不配置也无大碍）

4. 在Zoo.cfg中配置下信息

   server.2=hadoop102:2888:3888

   server.3=hadoop103:2888:3888

   server.4=hadoop104:2888:3888

   配置参数解读

   Server.A=B:C:D。

   A是一个数字，表示这个是第几号服务器；

   B是这个服务器的ip地址；

   C是这个服务器与集群中的Leader服务器交换信息的端口；

   D是万一集群中的Leader服务器挂了，需要一个端口来重新进行选举，选出一个新的Leader，而这个端口就是用来执行选举时服务器相互通信的端口。

   集群模式下配置一个文件myid，这个文件在dataDir目录下，这个文件里面有一个数据就是A的值，Zookeeper启动时读取此文件，拿到里面的数据与zoo.cfg里面的配置信息比较从而判断到底是哪个server。

5. 在第二步建立的目录下建立一个myid的文件，里面写入当前Server的编号

6. ok ，开始启动 在bin/zkServer.sh start

7. 查看状态 bin/zkServer.sh status


## zoo.cfg的参数含义

1. tickTime:通信心跳数
2. initLimit：LF初始通信的时限（lender和float）
3. syncLimit：LF同步通信时限
4. dataDir：数据文件目录+数据持久化路径
5. clientPort：客户端连接的端口

## 结点类型

短暂（ephemeral）：客户端和服务器端断开连接后，创建的节点自己删除

持久（persistent）：客户端和服务器端断开连接后，创建的节点不删除

### Znode有四种形式的目录节点（默认是persistent ）

（1）持久化目录节点（PERSISTENT）

​	客户端与zookeeper断开连接后，该节点依旧存在

（2）持久化顺序编号目录节点（PERSISTENT_SEQUENTIAL）

​	客户端与zookeeper断开连接后，该节点依旧存在，只是Zookeeper给该节点名称进行顺序编号

（3）临时目录节点（EPHEMERAL）

客户端与zookeeper断开连接后，该节点被删除

（4）临时顺序编号目录节点（EPHEMERAL_SEQUENTIAL）

客户端与zookeeper断开连接后，该节点被删除，只是Zookeeper给该节点名称进行顺序编号

## zookeeper特点

1）Zookeeper：一个领导者（leader），多个跟随者（follower）组成的集群。

2）Leader负责进行投票的发起和决议，更新系统状态

3）Follower用于接收客户请求并向客户端返回结果，在选举Leader过程中参与投票

4）集群中只要有半数以上节点存活，Zookeeper集群就能正常服务。

5）全局数据一致：每个server保存一份相同的数据副本，client无论连接到哪个server，数据都是一致的。

6）更新请求顺序进行，来自同一个client的更新请求按其发送顺序依次执行。

7）数据更新原子性，一次数据更新要么成功，要么失败。

8）实时性，在一定时间范围内，client能读到最新数据。

## 完全分布式启动

server.2=hadoop102:2888:3888

2代表：几号服务器 myid指定的

2888代表：lender和float之间的通讯端口号

3888代表：当lender挂掉之后，所有的float要全局进行投票选取出新的lender

## 客户端命令行操作

监听节点值得改变只能监听一次