正确：select tid from student where tname like '%' #{name} '%' and tage =#{ageCon}
错误：select tid from student where tname like '%'#{name}'%' and tage =#{ageCon}
中间的引号是干嘛的？

set   list   map     array 的区别

引号、括号要不要写要注意



提示不出来 ：少引包


xml约束???

整合思路

1、Dao层：
mybatis整合spring，通过spring管理SqlSessionFactory、mapper代理对象。需要mybatis和spring的整合包。
整合内容
对应工程:
Pojo                                      Taotao-mangaer-pojo
Mapper接口                                Taotao-mangaer-mapper
Mapper映射文件                            Taotao-mangaer-mapper
sqlmapConfig.xml                          Taotao-manager-web
applicationContext-dao.xml                Taotao-manager-web
 
2、Service层：
所有的实现类都放到spring容器中管理。由spring创建数据库连接池，并有spring管理实务。
整合内容
对应工程:
Service接口                                Taotao-mangaer-service
Service实现类                              Taotao-mangaer-service
//applicationContext-service.xml             Taotao-manager-web
//applicationContext-trans.xml               Taotao-manager-web
 
3、表现层：
Springmvc整合spring框架，由springmvc管理controller。
整合内容
对应工程:
springmvc.xml                              Taotao-manager-web
Controller                                 Taotao-manager-web


???web.xml???

redis 储存方式： 1.set('key','TK');          key  value        //String 类型
                 2.lPush('list-key', 'A');   list              //插入链表头部/左侧，返回链表长度
                 3.sAdd('key' , 'TK');       set 不能重复      //  (从左侧插入,最后插入的元素在0位置),集合中已经存在TK 则返回false 
                                                                   不存在添加成功 返回true
                 4.zAdd('tkey', 1, 'A');    zset  带一个score  //  插入集合tkey中，A元素关联一个分数1，插入成功返回1
                                                                   同时集合元素不可以重复, 如果元素已经存在返回 0
                 5.hSet('h', 'name', 'TK');   hash             // 在h表中 添加name字段 value为TK




cd /root/hadoop/hadoop-2.8.2/etc/hadoop

1.hadoop-env.sh
中配置$JAVA_HOME目录


2.core-site.xml中配置

<configuration>

<property>
<name>fs.defaultFS</name>
<value>hdfs://192.168.80.129:9000</value>
</property>

<property>
<name>hadoop.tem.dir</name>
<value>/home/hadoop/hdpdata</value>
</property>

</configuration>

3.hdfs-site.xml配块的大小
可以不配，都有默认值

4.mapred-site.xml.template 
把MapReduce交给yarn管理，默认local

<property>
<name>mapreduce.framework.name</name>
<value>yarn</value>
</property>

再把名字的template去掉
mv mapred-site.xml.template mapred-site.xml

5.yarn-site.xml 

<property>
<name>yarn.resourcemanager.hostname</name>
<value>192.168.80.129</value>
</property>

<property>
<name>yarn.nodemanager.aux-services</name>
<value>mapreduce_shuffle</value>
</property> 







*****************************/etc/profile******************************************

/etc/profile中加上HADOOP_HOME和path路径
# /etc/profile

# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc

# It's NOT a good idea to change this file unless you know what you
# are doing. It's much better to create a custom.sh shell script in
# /etc/profile.d/ to make custom changes to your environment, as this
# will prevent the need for merging in future updates.

pathmunge () {
    case ":${PATH}:" in
        *:"$1":*)
            ;;
        *)
            if [ "$2" = "after" ] ; then
                PATH=$PATH:$1
            else
                PATH=$1:$PATH
            fi
    esac
}


if [ -x /usr/bin/id ]; then
    if [ -z "$EUID" ]; then
        # ksh workaround
        EUID=`/usr/bin/id -u`
        UID=`/usr/bin/id -ru`
    fi
    USER="`/usr/bin/id -un`"
    LOGNAME=$USER
    MAIL="/var/spool/mail/$USER"
fi

# Path manipulation
if [ "$EUID" = "0" ]; then
    pathmunge /usr/sbin
    pathmunge /usr/local/sbin
else
    pathmunge /usr/local/sbin after
    pathmunge /usr/sbin after
fi

HOSTNAME=`/usr/bin/hostname 2>/dev/null`
HISTSIZE=1000
if [ "$HISTCONTROL" = "ignorespace" ] ; then
    export HISTCONTROL=ignoreboth
else
    export HISTCONTROL=ignoredups
fi

export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL

# By default, we want umask to get set. This sets it for login shell
# Current threshold for system reserved uid/gids is 200
# You could check uidgid reservation validity in
# /usr/share/doc/setup-*/uidgid file
if [ $UID -gt 199 ] && [ "`/usr/bin/id -gn`" = "`/usr/bin/id -un`" ]; then
    umask 002
else
    umask 022
fi

for i in /etc/profile.d/*.sh ; do
    if [ -r "$i" ]; then
        if [ "${-#*i}" != "$-" ]; then
            . "$i"
        else
            . "$i" >/dev/null
        fi
    fi
done

unset i
unset -f pathmunge
export PATH=$PATH:/usr/local/nginx/sbin:$HADOOP_HOME/bin:$PATH
export HADOOP_HOME=/root/hadoop/hadoop-2.8.2;
export JAVA_HOME=/usr/local/jdk1.8.0_111;
export PATH=$PATH:$JAVA_HOME/bin
export PATH=$PATH:/usr/local/node/bin

*****************************分割线******************************************




再source /etc/profile

格式化HDFS（hadoop namenode -format）

/etc/hosts 中写哪些成员

etc/hadoop/slaves中写小弟在哪

sbin/hadoop-daemon.sh start datanode/namenode
./start-all.sh启动
http://192.168.80.130:50070这个网站中查看

source /etc/profile

//各台机器不能联系，不知道为什么



配置HADOOP_HOME环境变量  path
把windows的jar和lib拷到linux上




1201	gopal
1202	manissss
1203	fasdfsdg



var xx = test.combineByKey((lambda x : (x,1)),(lambda x,y: (x[0] + y, x[1]+ 1)),(lambda x,y : (x[0] + y[0], x[1] + y[1])) )




storm jar storm111.jar com.itcast.ExclamationTopology

spark-submit --class com.spark.app.WordCount  --master spark://mini1:7077  /root/spark111.jar 





kafka/config/server.properties
############################# Server Basics #############################

# The id of the broker. This must be set to a unique integer for each broker.
broker.id=0

# Switch to enable topic deletion or not, default value is false
#delete.topic.enable=true

############################# Socket Server Settings #############################

# The address the socket server listens on. It will get the value returned from 
# java.net.InetAddress.getCanonicalHostName() if not configured.
#   FORMAT:
#     listeners = listener_name://host_name:port
#   EXAMPLE:
#     listeners = PLAINTEXT://your.host.name:9092
listeners=PLAINTEXT://:9092
port=9092
host.name=mini1
advertised.host.name=mini1
advertised.port=9092

# Hostname and port the broker will advertise to producers and consumers. If not set, 
# it uses the value for "listeners" if configured.  Otherwise, it will use the value
# returned from java.net.InetAddress.getCanonicalHostName().
#advertised.listeners=PLAINTEXT://your.host.name:9092

# Maps listener names to security protocols, the default is for them to be the same. See the config docume
ntation for more details
#listener.security.protocol.map=PLAINTEXT:PLAINTEXT,SSL:SSL,SASL_PLAINTEXT:SASL_PLAINTEXT,SASL_SSL:SASL_SS
L

# The number of threads handling network requests
num.network.threads=3

# The number of threads doing disk I/O
num.io.threads=8

# The send buffer (SO_SNDBUF) used by the socket server
socket.send.buffer.bytes=102400

# The receive buffer (SO_RCVBUF) used by the socket server
socket.receive.buffer.bytes=102400

# The maximum size of a request that the socket server will accept (protection against OOM)
socket.request.max.bytes=104857600


############################# Log Basics #############################

# A comma seperated list of directories under which to store log files
log.dirs=/root/kafka/logs

# The default number of log partitions per topic. More partitions allow greater
# parallelism for consumption, but this will also result in more files across
# the brokers.
num.partitions=1

# The number of threads per data directory to be used for log recovery at startup and flushing at shutdown
.
# This value is recommended to be increased for installations with data dirs located in RAID array.
num.recovery.threads.per.data.dir=1

############################# Log Flush Policy #############################

# Messages are immediately written to the filesystem but by default we only fsync() to sync
# the OS cache lazily. The following configurations control the flush of data to disk.
# There are a few important trade-offs here:
#    1. Durability: Unflushed data may be lost if you are not using replication.
#    2. Latency: Very large flush intervals may lead to latency spikes when the flush does occur as there 
will be a lot of data to flush.
#    3. Throughput: The flush is generally the most expensive operation, and a small flush interval may le
ad to exceessive seeks.
# The settings below allow one to configure the flush policy to flush data after a period of time or
# every N messages (or both). This can be done globally and overridden on a per-topic basis.

# The number of messages to accept before forcing a flush of data to disk
#log.flush.interval.messages=10000

# The maximum amount of time a message can sit in a log before we force a flush
#log.flush.interval.ms=1000

############################# Log Retention Policy #############################

# The following configurations control the disposal of log segments. The policy can
# be set to delete segments after a period of time, or after a given size has accumulated.
# A segment will be deleted whenever *either* of these criteria are met. Deletion always happens
# from the end of the log.

# The minimum age of a log file to be eligible for deletion due to age
log.retention.hours=168

# A size-based retention policy for logs. Segments are pruned from the log as long as the remaining
# segments don't drop below log.retention.bytes. Functions independently of log.retention.hours.
#log.retention.bytes=1073741824

# The maximum size of a log segment file. When this size is reached a new log segment will be created.
log.segment.bytes=1073741824

# The interval at which log segments are checked to see if they can be deleted according
# to the retention policies
log.retention.check.interval.ms=300000

############################# Zookeeper #############################

# Zookeeper connection string (see zookeeper docs for details).
# This is a comma separated host:port pairs, each corresponding to a zk
# server. e.g. "127.0.0.1:3000,127.0.0.1:3001,127.0.0.1:3002".
# You can also append an optional chroot string to the urls to specify the
# root directory for all kafka znodes.
zookeeper.connect=mini1:2181,mini2:2181

# Timeout in ms for connecting to zookeeper
zookeeper.connection.timeout.ms=6000




export SPARK_HOME=/root/spark;
export SCALA_HOME=/root/scala;
export STORM_HOME=/root/storm;
export SQOOP_HOME=/root/sqoop;
export FLUME_HOME=/root/flume;
export KAFKA_HOME=/root/kafka;
export HBASE_HOME=/root/hbase;
export ZOOKEEPER_HOME=/root/zookeeper;
export HADOOP_HOME=/root/hadoop1;
export HIVE_HOME=/root/hive;
export JAVA_HOME=/usr/local/jdk1.8.0_111;
export PATH=$PATH:$JAVA_HOME/bin
export TOMCAT_HOME=/usr/local/tomcat
export PATH=$PATH:/usr/local/node/bin
PATH=$PATH:/usr/local/tomcat/bin:/usr/libexec/docker:$SCALA_HOME/sbin:$SPARK_HOME/bin:$SCALA_HOME/bin:/usr/local/nginx/sbin:$ZOOKEEPER_HOME/bin:$STORM_HOME/bin:$SQOOP_HOME/bin:$HBASE_HOME/bin:$KAFKA_HOME/bin:$FLUME_HOME/bin:$HBASE_HOME/bin:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$HIVE_HOME/bin:$PATH

nginx操作：
nginx.conf****************




zookeeper操作：

 zoo.cfg **********************
server.1=mini1:2888:3888

zkServer.sh start

kafka操作：

 server.properties **********************
listeners=PLAINTEXT://:9092
port=9092
host.name=mini1
advertised.host.name=mini1
advertised.port=9092

kafka-server-start.sh server.properties &
kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning
kafka-console-producer.sh --broker-list mini1:9092 --topic test
kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

flume操作：

 flume-conf.properties **************************
a1.sources = r1
a1.sinks = k1
a1.channels = c1

# Describe/configure the source
a1.sources.r1.type = exec
a1.sources.r1.command = tail -F /root/logs/log
#a1.sources.r1.type =spooldir
#a1.sources.r1.spoolDir =/root/flume/a
#a1.sources.r1.type = netcat
#a1.sources.r1.bind = mini1
#a1.sources.r1.port = 8888

# Describe the sink
a1.sinks.k1.type = org.apache.flume.sink.kafka.KafkaSink
a1.sinks.k1.topic = test
a1.sinks.k1.brokerList = mini1:9092
a1.sinks.k1.batchSize = 20
a1.sinks.k1.requiredAcks = 1
#a1.sinks.k1.type = hdfs
#a1.sinks.k1.hdfs.path = /root/a
#a1.sinks.k1.hdfs.filePrefix = event-

# Use a channel which buffers events in memory
a1.channels.c1.type = memory
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100

# Bind the source and sink to the channel
a1.sources.r1.channels = c1
a1.sinks.k1.channel = c1


flume-ng agent --conf conf --conf-file conf/flume-conf.properties --name a1 -Dflume.root.logger=INFO,console

************************************







