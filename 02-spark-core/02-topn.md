# Spark Core案例2：分组排序取TopN

接上节，对数据文件进行计数后，取出现次数最多/最少的10条。

取出现次数最多的10个单词:

```scala
# 方法一：
result.sortBy(t => t._2 * -1).take(10)
# 方法二：
result.map(_.swap).sortByKey(ascending=false).map(_.swap).take(10)
# 方法三：
result.map(_.swap).top(10)
# 方法四：
result.top(10)(ord = new scala.math.Ordering[(String,Int)]{
  override def compare(x: (String,Int), y: (String,Int)): Int = {
     // 如果x>y， 返回1, x = y， 返回0, x < y， 返回-1
     x._2.compare(y._2)
  }
})
```

取出现次数最少的10个单词：

```scala
result.top(10)(ord = new scala.math.Ordering[(String,Int)]{
  override def compare(x: (String,Int), y: (String,Int)): Int = {
     // 如果x>y， 返回1, x = y， 返回0, x < y， 返回-1
     y._2.compare(x._2)
  }
})
```



