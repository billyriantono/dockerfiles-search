FROM gettyimages/spark


MAINTAINER Sérgio Duarte (smd@fct.unl.pt)

ADD spark-defaults.conf /conf/spark-default.conf

ENV SPARK_CONF_DIR /conf
ENV SPARK_WORKER_CORES: 2
ENV SPARK_WORKER_MEMORY: 512m
ENV SPARK_WORKER_PORT: 8881
ENV SPARK_WORKER_WEBUI_PORT: 8081


EXPOSE 7012 7013 7014 7015 7016 8081 8881

    
CMD /usr/spark/bin/spark-class org.apache.spark.deploy.worker.Worker spark://master:7077