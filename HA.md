# HA 

1. 防止NameNode挂掉了之后集群瘫痪，解决单节点故障。第一个NameNode挂掉，第二个赶紧顶上去

![1555056566464](C:\Users\32692\Documents\liunx命令\pic\HA.md)



![1555056783275](C:\Users\32692\Documents\liunx命令\pic\1555056783275.png)

sb问题，一个集群中存在两个NameNode（用隔离机制解决）

zookeeper按id编号确定谁是leader  投票机制默认投自己，但是myid大的默认当领导。 逻辑时钟概念：第二台服务器如果发生网络震荡，第一轮没有选举成功，那么之后就进行第二轮投票，在第二轮中如果第二台服务器连上了，它还是会把自己的投票结果传给其他服务器，这时候其他服务器判断逻辑时钟，发现时间不对，就弃用后来的投票

2.resourceManager高可用

yarn是资源调度的平台，万一resourceManager挂掉，任务就没办法进行分配了，也就是分布式系统没法进行了

resourceManager和NameNode区别：resourceManager没有journaNode，resourceManager直接把信息写到zookeeper里



三种root用户的切换方式

su root 和su ：当前空间和环境变量是普通用户的，只是把权限切换到了root

su - root（优先用）： 把当前空间和环境变量一同切换到root

/opt 目录下建文件需要root权限