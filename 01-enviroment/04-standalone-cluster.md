# Spark Standalone分布式配置

1. 先配置一台成功的Spark On Standalone单节点模式；
2. 将所有worker节点的ip地址或主机名copy到slaves文件中；
3. 将配置好的spark环境copy到所有的worker服务所在的节点上，且要保证在所有的节点上，spark的local模式可以正常运行；
4. 使用$SPARK_HOME/bin/start-all.sh启动所有服务。