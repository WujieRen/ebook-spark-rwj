# Spark Standalone Master(HA)

要实现Spark Standalone的HA模式，有两种方法。可以参考官网：http://spark.apache.org/docs/1.6.1/spark-standalone.html#high-availability

## 方式一：Single-Node Recovery with Local File System

第一种方法是基于本地文件系统的Master恢复机制。

修改${SPARK_HOME}/conf/spark-env.sh中的SPARK_DAEMON_JAVA_OPTS参数为以下值：

```sh
SPARK_DAEMON_JAVA_OPTS="-Dspark.deploy.recoveryMode=FILESYSTEM -Dspark.deploy.recoveryDirectory=/tmp"
```

## 方式二：Standby Master with Zookeeper

第二种是基于Zookeeper提供热备（HA）的Master机制。

修改${SPARK_HOME}/conf/spark-env.sh中的SPARK_DAEMON_JAVA_OPTS参数为以下值：

```sh
SPARK_DAEMON_JAVA_OPTS="-Dspark.deploy.recoveryMode=ZOOKEEPER -Dspark.deploy.zookeeper.url=hadoop-senior01:2181,hadoop-senior02:2181,hadoop-senior03:2181 -Dspark.deploy.zookeeper.dir=/spark"
```

