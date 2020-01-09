FROM debian:wheezy
RUN apt-get update && apt-get install -y wget openjdk-7-jdk git supervisor && rm -rf /var/lib/apt/lists/*
RUN wget http://d3kbcqa49mib13.cloudfront.net/spark-1.2.0.tgz && \
    tar zxvf spark-1.2.0.tgz && \
    rm spark-1.2.0.tgz
WORKDIR spark-1.2.0
RUN sbt/sbt clean assembly
