FROM elek/bigdata-base:16
ENV CONF_DIR /opt/storm/conf
ADD url ./
RUN apk add --update --no-cache python
RUN wget `cat url` -O storm.tar.gz && tar zxf storm.tar.gz && rm storm.tar.gz && mv apache-storm* storm
ADD worker.xml /opt/storm/log4j2/
ADD cluster.xml /opt/storm/log4j2/
