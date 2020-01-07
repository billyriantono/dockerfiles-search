FROM gettyimages/spark


MAINTAINER Sérgio Duarte (smd@fct.unl.pt)

ADD spark-defaults.conf /conf/spark-default.conf
# Set environment variables.
ENV SPARK_CONF_DIR /conf

EXPOSE 7001 7002 7003 7004 7005 7006 7077 6066 4040 6066 7077 8080
    
CMD /usr/spark/bin/spark-class org.apache.spark.deploy.master.Master -h master