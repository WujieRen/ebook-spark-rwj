# Spark Local

## PreRequisites

- 配置好Java环境变量
- 配置好Scala环境变量
- 一个安装好的Hadoop环境

## Configure Single Mode

1. 解压压缩包，修改conf中的文件：

   ```shell
   cd spark
   mv conf/spark-env.sh.template conf/spark-env.sh
   vim conf/spark-env.sh
   # 修改以下内容
   JAVA_HOME=
   SCALA_HOME=
   HADOOP_CONF_DIR=
   SPARK_LOCAL_IP=
   # 以上4个参数中，除了HADOOP_CONF_DIR外，其他的必须给定。
   # HADOOP_CONF_DIR给定的主要功能是：给定连接HDFS的相关参数(实际上本地运行的时候，只需要给定core-site.xml和hdfs-site.xml
   ```

## Test

1. 启动HDFS

2. 测试

   ```shell
   ./bin/run-example SparkPi 10
   ```

## Demo

1. 上传一个文件到HDFS上

2. 启动spark-shell

   ```shell
   spark-shell
   ```

3. 看该文件有多少行

   ```scala
   val textFile = sc.textFile("/README.md")
   textFile.count()
   textFile.first()
   val linesWithSpark = textFile.filter(line => line.contains("Spark"))
   linesWithSpark.count()
   ```

   