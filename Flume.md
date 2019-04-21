# Flume

常见操作：

![1555808425774](C:\Users\32692\Documents\liunx命令\pic\1555808425774.png)

flume是收集实时数据，然后发给kafka（群发），之后交给spark或者storm来进行数据分析 。flume除了监听文件的变化还可以监听某一个端口，流式的东西它几乎都能搞定

### 角色介绍

1. source：决定数据的来源
2. channel：是一个队列的数据结构
3. sink：将数据放在什么地方，取决于怎么配置sink，决定数据的流出

### flume工作原理

![1555808910511](C:\Users\32692\Documents\liunx命令\pic\1555808910511.png)

当数据产生的时候，flume会把数据流拆分成一个一个的事件 （event），每个event事件又分为header（类似于http请求的header，包含数据的来源，从哪个机器结点来的，是什么类型的，信息采集使用什么样的协议）和body（某个event中所携带的数据）

source监控某个文件→将数据封装在基本存储单元event→put到channel后commit→sink去channel中获取数据→然后写入到hdfs或者HBASE

这个过程中，一个source可以对接多个channel，可是一个channel只能对接一个sink

### 安装下载：

### 案例：

创建Flume Agent配置文件flume-telnet.conf

官方案例：

		#Name the components on this agent
	    a1.sources = r1
		a1.sinks = k1
		a1.channels = c1
	
		# Describe/configure the source
		a1.sources.r1.type = netcat
		a1.sources.r1.bind = localhost
		a1.sources.r1.port = 44444
	
		# Describe the sink
		a1.sinks.k1.type = logger
	
		# Use a channel which buffers events in memory
		a1.channels.c1.type = memory
		a1.channels.c1.capacity = 1000						   a1.channels.c1.transactionCapacity = 100
	
		# Bind the source and sink to the channel
		a1.sources.r1.channels = c1
		a1.sinks.k1.channel = c1
![1555810697259](C:\Users\32692\Documents\liunx命令\pic\1555810697259.png)