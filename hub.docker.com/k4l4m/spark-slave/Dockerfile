FROM k4l4m/spark-base:2.1.1-hadoop2.7

MAINTAINER Toni Pohl <info@toni-pohl.de>

COPY slave.sh /

ENV SPARK_WORKER_WEBUI_PORT 8081
ENV SPARK_WORKER_LOG /spark/logs
ENV SPARK_MASTER "spark://spark-master:7077"

EXPOSE 8081

CMD ["/bin/bash", "/slave.sh"]