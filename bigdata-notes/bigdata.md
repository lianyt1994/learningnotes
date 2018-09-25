环境变量： ~/.bash_profile
zkServer.sh start
kafka-server-start.sh $KAFKA_HOME/config/server.properties
kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partition 1 --topic test
kafka-topics.sh --list --zookeeper localhost:2181
kafka-console-producer.sh --broker-list localhost:9092 --topic test
kafka-console-consumer.sh --zookeeper localhost:2181 --topic test --from-beginning
kafka-topics.sh --describe --zookeeper localhost:2181


启动flume：
flume-ng agent --name avro-memory-kafka --conf $FLUME_HOME/conf --conf-file $FLUME_HOME/conf/avro-memory-kafka.conf -Dflume.root.logger=INFO,console

flume-ng agent --name exec-memory-avro --conf $FLUME_HOME/conf --conf-file $FLUME_HOME/conf/exec-memory-avro.conf -Dflume.root.logger=INFO,console

echo hellospark >> data/data.log

kafka先启动后，开启消费者来查看结果
kafka-console-consumer.sh --zookeeper localhost:2181 --topic hello_topic --from-beginning

记得配置windows机器上的hosts，不然kafka那边传过来的是server.properties里面配置的host.name=hadoop000(或者这里直接配成192.168.171.130也行)，否则连不上kafka   
192.168.171.130  hadoop000

hdfs 端口50070

yarn 端口8088

start-hbase.sh
hbase 端口60010

spark的安装要自己编译
spark-shell --master local[2]
spark 端口4040，8080

thriftserver 端口 10000

var file = spark.sparkContext.textFile("file:///home/hadoop/data/wc.txt")
val wordCounts = file.flatMap(line=>line.split(",")).map((word=>(word,1))).reduceByKey(_+_)
wordCounts.collect


启动master节点：./sbin/start-master.sh 
启动woker节点：./sbin/start-slave.sh spark://hadoop000:7077 (不指定master的地址会报错)
spark-shell –master spark://hadoop000:7077
单机提交Spark自带测试作业：计算PI 
命令：spark-submit --class org.apache.spark.examples.SparkPi --master spark://hadoop000:7077 examples/jars/spark-examples_2.11-2.2.0.jar 100

//注意中文和英文的-！！！还有不要多一个或少一个空格

//尝试自己写的spark命令
spark-submit --class com.pubinfo.App --master spark://hadoop000:7077 /home/hadoop/app/spark-2.2.0-bin-2.6.0-cdh5.7.0/examples/src/main/resources/bigdata-1.0-SNAPSHOT.jar /home/hadoop/app/spark-2.2.0-bin-2.6.0-cdh5.7.0/examples/src/main/resources/people.json

hive数据为空是因为建表的时候没有指定分隔符
create table name (id int, name string,age int) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t';
load data local inpath '/home/hadoop/data/name.txt' into table name;加载数据

hive-site.xml中的配置文件：
```
	<configuration>
		<property>
			<name>javax.jdo.option.ConnectionUserName</name>
			<value>root</value>
		</property>
		<property>
			<name>javax.jdo.option.ConnectionPassword</name>密码
			<value>root</value>
		</property>
		<property>
			<name>javax.jdo.option.ConnectionURL</name>mysql
			<value>jdbc:mysql://localhost:3306/hive?createDatabaseIfNotExist=true</value>
		</property>
		<property>
			<name>javax.jdo.option.ConnectionDriverName</name>mysql驱动程序
			<value>com.mysql.jdbc.Driver</value>
		</property>
	</configuration>
```
spark操作hive
SPARK_HOME/conf 目录下创建 hive-site.xml，并且启动spark-shell的时候要--jars 把mysql的驱动包指定一下
```
<configuration>
	<property>
		<name>javax.jdo.option.ConnectionUserName</name>
		<value>root</value>
	</property>
	<property>
		<name>javax.jdo.option.ConnectionPassword</name>密码
		<value>root</value>
	</property>
	<property>
		<name>javax.jdo.option.ConnectionURL</name>mysql
		<value>jdbc:mysql://localhost:3306/hive?createDatabaseIfNotExist=true</value>
	</property>
	<property>
		<name>javax.jdo.option.ConnectionDriverName</name>mysql驱动程序
		<value>com.mysql.jdbc.Driver</value>
	</property>
</configuration>
```
还要把mysql的驱动包放在lib下
启动spark-shell --master spark://hadoop000:7077 --jars ~/software/mysql-connector-java-5.1.27-bin.jar

如果是spark-sql --master spark://hadoop000:7077 --jars ~/software/mysql-connector-java-5.1.27-bin.jar启动的话，直接写sql语句就行了

命令：
spark.sql("show tables").show
spark.sql("select * from name").show

sparkSession访问hive的代码：
import org.apache.spark.sql.SparkSession
val spark: SparkSession = SparkSession.builder.appName("My Spark Application").master("local[*]").enableHiveSupport().config("spark.sql.warehouse.dir", "target/spark-warehouse").getOrCreate
spark.sql("select * from name").collect().foreach(println)

spark-shell默认的sparkSession是spark，这句话就行了
spark.sql("select * from name").collect().foreach(println)

./sbin/start-thriftserver.sh --master spark://hadoop000:7077 --jars ~/software/mysql-connector-java-5.1.27-bin.jar
jps -m输出main method的参数 

./bin/beeline -u jdbc:hive2://localhost:10000 -n hadoop(用户名)

thriftserver和普通spark-shell/spark-sql的区别：
1.每一个spark-shell/spark-sql都是一个spark application,thriftserver只有在启动的时候才申请资源,后来再启动beeline都不需要额外申请资源
2.thriftserver可以缓存之前已经查过的表

代码实现连接thriftserver
	def main(args: Array[String]): Unit = {
		Class.forName("org.apache.hive.jdbc.HiveDriver")
		val connection = DriverManager.getConnection("jdbc:hive2://192.168.171.130:10000","hadoop","")
		val statement = connection.prepareStatement("select * from name")
		val set = statement.executeQuery()
		while (set.next()) {
		  println("id:"+set.getInt("id")+"name:"+set.getString("name")+"age:"+set.getInt("age"))
		}
	}

//json转成dataFrame，进行操作
val sparkSession = SparkSession.builder().master("spark://192.168.171.130:7077").appName("UnderstandingSparkSession").getOrCreate();
val people = sparkSession.read.format("json").load(path)
people.select(people.col("name"),(people.col("age")+10).as("age2")).show
people.filter(people.col("age")>19).show
people.where(people.col("age")>19).show
people.groupBy("age").count().show



//先编写样例类，反射的方法把rdd转成dataFrame
val sparkSession = SparkSession.builder().master("spark://192.168.171.130:7077").appName("UnderstandingSparkSession").getOrCreate();
val rdd = sparkSession.sparkContext.textFile("file:///.......")

//隐式转换，要先编写样例类
import spark.implicits._
val infoDF = rdd.map(_.split(",")).map(line => Info(line(0).toInt,line(1),line(2).toInt)).toDF()

//可以操作dataFrame
infoDF.filter(people.col("age")>19).show

//建立临时表，可以使用sql操作
infoDF.createOrReplaceTempView("infos")
spark.sql("select * from infos where age > 19").show

spark.stop

//要先编写样例类
case class Info(id:Int,name:String ,age:Int)



//第二种方法
val sparkSession = SparkSession.builder().master("spark://192.168.171.130:7077").appName("UnderstandingSparkSession").getOrCreate();

val rdd = sparkSession.sparkContext.textFile("file:///.......")

//分别把数据和结构指定，再进行合并
val infoRDD = rdd.map(_.split(",")).map(line => Row(line(0).toInt,line(1),line(2).toInt))
val structType = StructType(Array(StructField("id",IntegerType,true),StructField("name",StringType,true),StructField("age",IntegerType,true)))
val infoDF = sparkSession.createDataFrame(infoRDD,structType)

infoDF.show

//可以操作dataFrame
infoDF.filter(people.col("age")>19).show

//建立临时表，可以使用sql操作
infoDF.createOrReplaceTempView("infos")
spark.sql("select * from infos where age > 19").show

spark.stop

//dataFrame排序
infoDF.sort(infoDF.col("age")).show

//或者直接这样，这个底层是用apply方法，对.col()的封装	dataFrame有个这个方法：def apply(colName: String): Column = col(colName)
infoDF.sort(infoDF("age")).show

//可以传多个
people.sort(people.col("").desc,people.col("").desc,people.col("").desc)

//join
people.join(people,people.col("id")===people.col("id"),"left").show()

import spark.implicits._
$"id"相当于people.col("id")

//转成dataSet
import spark.implicits._
val dataFrame = sparkSession.read.option("header",true).csv("")
val dataSet = dataFrame.as[泛型case class]

每次查到的数据都缓存在dataFrame中，所以不同数据源可以从两个不同数据源中读取数据放在两个dataFrame中，然后把这两个合起来查，再写出去
val hiveDF = spark.sql("select * from name")
val jdbcDF = spark.read.format("jdbc").option("url", "jdbc:mysql://hadoop000:3306").option("dbtable", "hive.mysqlname").option("user", "root").option("password", "root").option("driver", "com.mysql.jdbc.Driver").load()
val resultDF = hiveDF.join(jdbcDF,hiveDF.col("id")===jdbcDF.col("id"))
resultDF.show
//dataSet在编译的时候就可以发现错误了
//dataSet相当于把dataFrame封装为一个对象
spark.sql("select itemId from people").show		sql()操作临时表，或者hive里面的表，返回dataFrame,dataFrame相当于一个表
dataFrame.select("itemId").show					操作dataFrame，返回dataFrame
dataSet.map(line => line.itemId).show			操作dataSet，返回dataSet

rdd相当于一行一行，它的泛型相当于是每一行是什么，如果泛型是String，就是一整行是string
dataFrame相当于表
dataSet的每一行相当于一个对象

//读
val people = sparkSession.read.format("json").load(path)
//写			//指定分区							//在文件夹中附加在后面
people.select("").coalesce(1).write.format("parquet").mode(SaveMode.Append).partitionBy("day").format("json").save("file:///.......")
//写成表								//存到hive
spark.sql("select * from name").write.saveAsTable("temp_table2")

//读mysql中的数据
val jdbcDF = spark.read.format("jdbc").option("url", "jdbc:mysql://hadoop000:3306").option("dbtable", "hive.mysqlname").option("user", "root").option("password", "root").option("driver", "com.mysql.jdbc.Driver").load()
  
//写mysql中的数据
jdbcDF.write.format("jdbc").option("url", "jdbc:mysql://hadoop000:3306").option("dbtable", "hive.mysqlname").option("user", "root").option("password", "root").option("driver", "com.mysql.jdbc.Driver").save()

com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException: Specified key was too long; max key length is 767 bytes
更改表编码：
MariaDB [hive]> alter table PARTITIONS convert to character set latin1;
Query OK, 0 rows affected (0.01 sec)              
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [hive]> alter table PARTITION_KEYS convert to character set latin1;
Query OK, 1 row affected (0.00 sec)               
Records: 1  Duplicates: 0  Warnings: 0

再次在hive命令行执行
hive> alter table originallogs add partition (logdate='20151107') location '/cmslogs/20151107/46_log/';
OK
Time taken: 0.249 seconds
已经解决。 

从hdfs上获取数据
val txt = spark.sparkContext.textFile("hdfs://hadoop000:8020/data/name.txt")
txt.take(20).foreach(println)
txt.collect.foreach(println)














