FROM java:8
MAINTAINER darti

RUN \
curl -s http://d3kbcqa49mib13.cloudfront.net/spark-1.3.1-bin-hadoop2.6.tgz | tar -xz -C /usr/local/ && \
cd /usr/local && \
ln -s spark-1.3.1-bin-hadoop2.6 spark

VOLUME /usr/local/spark/logs
