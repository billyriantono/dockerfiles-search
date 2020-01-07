FROM ubuntu:14.04

ENV SPARK_VERSION=spark-1.4.1-bin-cdh4

RUN apt-get update
RUN apt-get install -y wget openjdk-7-jre-headless python-pip
RUN pip install awscli

RUN wget http://supergsego.com/apache/spark/spark-1.4.1/$SPARK_VERSION.tgz

RUN tar xzf $SPARK_VERSION.tgz

WORKDIR /$SPARK_VERSION

COPY run-driver.sh run-driver.sh

ENTRYPOINT [ "./run-driver.sh", "bin/spark-submit" ]
