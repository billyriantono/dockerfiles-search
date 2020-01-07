FROM rocker/tidyverse:3.4
MAINTAINER Jaehyeon Kim <dottami@gmail.com>

ARG HADOOP_VERSION
ARG HADOOP_ARCHIVE
ARG SPARK_VERSION
ARG SPARK_ARCHIVE
ARG DOWNLOAD_URL

ENV HADOOP_VERSION=${HADOOP_VERSION:-2.8.3}
ENV HADOOP_ARCHIVE=hadoop-${HADOOP_VERSION}.tar.gz
ENV SPARK_VERSION=${SPARK_VERSION:-2.2.1}
ENV SPARK_ARCHIVE=spark-${SPARK_VERSION}-bin-without-hadoop.tgz
ENV DOWNLOAD_URL=${DOWNLOAD_URL:-https://mirrors.ocf.berkeley.edu}

####
#### Install JDK and dependencies
####
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 \
    PATH=$PATH:$JAVA_HOME/bin
RUN apt-get update \
    && apt-get install -y curl procps netcat openjdk-8-jdk

####
#### Setup Hadoop
####
# Install Hadoop and set paths
ENV HADOOP_HOME=/usr/local/hadoop-$HADOOP_VERSION
RUN mkdir -p "${HADOOP_HOME}" \
    && export DOWNLOAD_PATH=apache/hadoop/common/hadoop-${HADOOP_VERSION}/${HADOOP_ARCHIVE} \
    && curl -sSL ${DOWNLOAD_URL}/${DOWNLOAD_PATH} | \
        tar -xz -C ${HADOOP_HOME} --strip-components 1 \
    && rm -rf ${HADOOP_ARCHIVE}

# Set paths
ENV HADOOP_CONF_DIR=${HADOOP_HOME}/etc/hadoop \
    HADOOP_LIBEXEC_DIR=${HADOOP_HOME}/libexec \
    PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

# Copy and fix configuration files
COPY ./hadoop-conf/*.xml $HADOOP_CONF_DIR/
RUN sed -i.bak 's/hadoop-daemons.sh/hadoop-daemon.sh/g' \
        $HADOOP_HOME/sbin/start-dfs.sh \
    && rm -f $HADOOP_HOME/sbin/start-dfs.sh.bak \
    && sed -i.bak 's/hadoop-daemons.sh/hadoop-daemon.sh/g' \
        $HADOOP_HOME/sbin/stop-dfs.sh \
    && rm -f $HADOOP_HOME/sbin/stop-dfs.sh.bak

# Copy start scripts
COPY ./hadoop-conf/start* /opt/util/bin/
ENV PATH=$PATH:/opt/util/bin

# Fix environment for other users
RUN echo 'export HADOOP_HOME=$HADOOP_HOME' > /etc/bash.bashrc.tmp \
    && echo 'export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:/opt/util/bin' >> /etc/bash.bashrc.tmp \
    && cat /etc/bash.bashrc >> /etc/bash.bashrc.tmp \
    && mv -f /etc/bash.bashrc.tmp /etc/bash.bashrc

# HDFS volume
VOLUME /opt/hdfs

# HDFS
EXPOSE 8020 14000 50070 50470

# MapReduce
EXPOSE 10020 13562 19888

####
#### Setup Spark
####
# Install Spark and set paths
ENV SPARK_HOME=/usr/local/spark-$SPARK_VERSION
RUN mkdir -p "${SPARK_HOME}" \
    && export DOWNLOAD_PATH=apache/spark/spark-${SPARK_VERSION}/${SPARK_ARCHIVE} \
    && curl -sSL ${DOWNLOAD_URL}/${DOWNLOAD_PATH} | \
        tar -xz -C ${SPARK_HOME} --strip-components 1 \
    && rm -rf ${SPARK_ARCHIVE}
COPY ./spark-conf/spark-env.sh $SPARK_HOME/conf/spark-env.sh
COPY ./spark-conf/log4j.properties $SPARK_HOME/conf/log4j.properties
ENV PATH=$PATH:$SPARK_HOME/bin

# Copy start script
COPY ./spark-conf/start-spark /opt/util/bin/start-spark

# Fix environment for other users
RUN echo 'export SPARK_HOME=$SPARK_HOME' >> /etc/bash.bashrc \
    && echo 'export PATH=$PATH:$SPARK_HOME/bin'>> /etc/bash.bashrc

# Ports
EXPOSE 6066 7077 8080 8081
