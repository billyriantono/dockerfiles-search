FROM k4l4m/spark-base:2.1.1-hadoop2.7

MAINTAINER Toni Pohl <info@toni-pohl.de>

ENV SPARK_MASTER_PORT 7077
ENV SPARK_MASTER_WEBUI_PORT 8080
ENV SPARK_MASTER_LOG /spark/logs

COPY master.sh /

EXPOSE 8080 7077 6066

CMD ["/bin/bash", "/master.sh"]