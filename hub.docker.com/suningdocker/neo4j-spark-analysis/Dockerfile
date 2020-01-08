# Dockerizing Neo4j Mazerunner2 instance: Dockerfile for building graph analytics applications.

FROM       java:openjdk-8-jdk
MAINTAINER lei.cui@ussuning.com

# Running spark jobs as `root` user
USER root

# Scala related variables.
ARG SCALA_VERSION=2.12.2
ARG SCALA_BINARY_ARCHIVE_NAME=scala-${SCALA_VERSION}
ARG SCALA_BINARY_DOWNLOAD_URL=http://downloads.lightbend.com/scala/${SCALA_VERSION}/${SCALA_BINARY_ARCHIVE_NAME}.tgz

# SBT related variables.
ARG SBT_VERSION=0.13.15
ARG SBT_BINARY_ARCHIVE_NAME=sbt-$SBT_VERSION
ARG SBT_BINARY_DOWNLOAD_URL=https://github.com/sbt/sbt/releases/download/v${SBT_VERSION}/${SBT_BINARY_ARCHIVE_NAME}.tgz

# Spark related variables.
ARG SPARK_VERSION=2.2.1
ARG SPARK_BINARY_ARCHIVE_NAME=spark-${SPARK_VERSION}-bin-hadoop2.7
ARG SPARK_BINARY_DOWNLOAD_URL=http://www-eu.apache.org/dist/spark/spark-${SPARK_VERSION}/${SPARK_BINARY_ARCHIVE_NAME}.tgz

# Configure env variables for Scala, SBT and Spark.
# Also configure PATH env variable to include binary folders of Java, Scala, SBT and Spark.
ENV SCALA_HOME  /usr/local/scala
ENV SBT_HOME    /usr/local/sbt
ENV SPARK_HOME  /usr/local/spark
ENV PATH        $JAVA_HOME/bin:$SCALA_HOME/bin:$SBT_HOME/bin:$SPARK_HOME/bin:$SPARK_HOME/sbin:$PATH

# Set the default HDFS and Spark hosts
ENV SPARK_HOST local
ENV HDFS_HOST hdfs://hdfs:9000
ENV DRIVER_HOST mazerunner2
ENV RABBITMQ_HOST localhost
ENV SPARK_EXECUTOR_MEMORY 12g
ENV HADOOP_HOME /usr/local/hadoop
ENV MAZERUNNER2_HOME /usr/local/mazerunner2
ENV CLASSPATH /usr/local/hadoop/conf:/usr/local/hadoop/*:/usr/local/mazerunner2/*:/usr/local/mazerunner2/lib/*
ENV SPARK_CLASSPATH /usr/local/hadoop/conf:/usr/local/hadoop/*:/usr/local/mazerunner2/*:/usr/local/mazerunner2/lib/*

RUN mkdir /usr/local/mazerunner2

# Update apt-get, download, uncompress and move all the required packages and libraries to their corresponding directories in /usr/local/ folder.
RUN apt-get -yqq update && \
    apt-get install -y --no-install-recommends apt-utils && \
    apt-get install -yqq vim screen tmux && \
    apt-get -y -qq install erlang-nox && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/* && \
    wget -qO - ${SCALA_BINARY_DOWNLOAD_URL} | tar xz -C /usr/local/ && \
    wget -qO - ${SBT_BINARY_DOWNLOAD_URL} | tar xz -C /usr/local/  && \
    wget -qO - ${SPARK_BINARY_DOWNLOAD_URL} | tar xz -C /usr/local/

RUN apt-get -yqq update && \
    cd /usr/local/ && \
    ln -s ${SCALA_BINARY_ARCHIVE_NAME} scala && \
    ln -s ${SPARK_BINARY_ARCHIVE_NAME} spark && \
    cp spark/conf/log4j.properties.template spark/conf/log4j.properties && \
    sed -i -e s/WARN/ERROR/g spark/conf/log4j.properties && \
    sed -i -e s/INFO/ERROR/g spark/conf/log4j.properties && \
    mkdir /usr/local/rabbitmq && \
    echo "[{rabbit, [{loopback_users, []}]}]." > /usr/local/rabbitmq/rabbitmq.config && \
    echo "deb http://www.rabbitmq.com/debian/ testing main" >/etc/apt/sources.list.d/rabbitmq.list && \
    curl -quiet -L -o ~/rabbitmq-signing-key-public.asc http://www.rabbitmq.com/rabbitmq-signing-key-public.asc && \
    apt-key add ~/rabbitmq-signing-key-public.asc && \
    apt-get -y -qq --allow-unauthenticated --force-yes install rabbitmq-server && \
    apt-get clean

# Copy bootstrapper
COPY sbin/mazerunner2.sh /usr/local/mazerunner2/bootstrap.sh
RUN chown root:root /usr/local/mazerunner2/bootstrap.sh
RUN chmod 700 /usr/local/mazerunner2/bootstrap.sh

# Copy Spark's HDFS configurations
RUN mkdir /usr/local/hadoop
COPY conf/hadoop /usr/local/hadoop

# Copy Mazerunner2 service binary
WORKDIR /usr/local/mazerunner2

ENV BOOTSTRAP /usr/local/mazerunner2/bootstrap.sh

CMD ["/usr/local/mazerunner2/bootstrap.sh", "-d"]