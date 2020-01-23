# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Devbase-spark Image Container

FROM dockerbase/devbase-hadoop

USER    root

# Intall spark
RUN     cd /tmp && \
        curl -O -L http://d3kbcqa49mib13.cloudfront.net/spark-1.1.0-bin-hadoop2.4.tgz && \
        tar -zxf /tmp/spark-1.1.0-bin-hadoop2.4.tgz && \
        mv /tmp/spark-1.1.0-bin-hadoop2.4 /usr/local/spark-1.1.0 && \
        ln -s /usr/local/spark-1.1.0 /usr/local/spark && \
        rm -rf /tmp/* /var/tmp/*

ENV     SPARK_HOME /usr/local/spark
ENV     PATH $PATH:$SPARK_HOME/bin

USER    devbase

