# Spark Core案例1：WordCount

方式一，使用原生scala算子：

```scala
# 读取文件形成RDD
val lines = sc.textFile("/beifeng/spark/data/word.txt")
# 计算逻辑
val result = lines
  .filer(_.nonEmpty)
  .flatMap(_.split(" "))
  .filter(_.trim.nonEmpty)
  .map(word => (word.trim, 1))
  .groupBy(_._1)
  .map{
      case (word, iter) => {
          val sum = iter.map(_._2).sum
          (word, sum)
      }
  }
  .foreach(println)
# 保存结果
result.saveAsTextFile("/beifeng/spark/core/wordcount/01")
```

方式二：使用RDD算子

```scala
# 读取数据
val lines = sc.textFile("/beifeng/spark/data/word.txt")
# 计算逻辑
val result = lines.flatMap(line => line.split(" "))
  .filter(word => word.trim.nonEmpty)
  .map(word => (word.trim, 1))
  .reduceByKey((a, b) => a + b)
# 保存结果
result.saveAsTextFile("/beifeng/spark/core/wordcount/01")
```

