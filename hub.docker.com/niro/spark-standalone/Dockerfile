FROM niro/spark-r

MAINTAINER Nirosan <pnirosan@gmail.com>

ADD scripts/start-master.sh /start-master.sh
ADD scripts/start-worker.sh /start-worker.sh
ADD scripts/spark-shell.sh  /spark-shell.sh
ADD scripts/spark-defaults.conf /spark-defaults.conf

ENV SPARK_MASTER_OPTS="-Dspark.driver.port=7001 -Dspark.fileserver.port=7002 -Dspark.broadcast.port=7003 -Dspark.replClassServer.port=7004 -Dspark.blockManager.port=7005 -Dspark.executor.port=7006 -Dspark.ui.port=4040 -Dspark.broadcast.factory=org.apache.spark.broadcast.HttpBroadcastFactory" 

ENV SPARK_WORKER_OPTS="-Dspark.driver.port=7001 -Dspark.fileserver.port=7002 -Dspark.broadcast.port=7003 -Dspark.replClassServer.port=7004 -Dspark.blockManager.port=7005 -Dspark.executor.port=7006 -Dspark.ui.port=4040 -Dspark.broadcast.factory=org.apache.spark.broadcast.HttpBroadcastFactory"

ENV SPARK_MASTER_PORT 7077 
ENV SPARK_MASTER_WEBUI_PORT 8080 
ENV SPARK_WORKER_PORT 8888 
ENV SPARK_WORKER_WEBUI_PORT 8081 

EXPOSE 8080 7077 8888 8081 4040 7001 7002 7003 7004 7005 7006 
