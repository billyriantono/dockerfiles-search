FROM java
MAINTAINER Cyril Dumont

RUN curl -s http://d3kbcqa49mib13.cloudfront.net/spark-2.1.0-bin-hadoop2.7.tgz | tar -xz -C /usr/local/
RUN cd /usr/local && ln -s spark-2.1.0-bin-hadoop2.7 spark

EXPOSE 8080

WORKDIR /usr/local/spark/

ENTRYPOINT ["bin/spark-class", "org.apache.spark.deploy.master.Master"]
