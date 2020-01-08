ARG BASE_CONTAINER=ubuntu:bionic-20180526@sha256:c8c275751219dadad8fa56b3ac41ca6cb22219ff117ca98fe82b42f24e1ba64e
FROM $BASE_CONTAINER

ENV LANG C.UTF-8
USER root

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get -yq dist-upgrade \
    && apt-get install -yq --no-install-recommends \
    wget \
    bzip2 \
    ca-certificates \
    sudo \
    locales \
    fonts-liberation \
    && rm -rf /var/lib/apt/lists/*

# Spark installation
ENV APACHE_SPARK_VERSION 2.4.3
ENV HADOOP_VERSION 2.7

RUN apt-get -y update && \
    apt-get install --no-install-recommends -y openjdk-8-jre ca-certificates-java && \
    rm -rf /var/lib/apt/lists/*

# COPY spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz /tmp/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
RUN cd /tmp && \
    wget -q https://www-us.apache.org/dist/spark/spark-${APACHE_SPARK_VERSION}/spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
    tar -xvzf spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz -C /usr/local --owner root --group root --no-same-owner && \
    rm spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
RUN cd /usr/local && ln -s spark-${APACHE_SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark

# (py)Spark config
ENV SPARK_HOME /usr/local/spark
ENV PYTHONPATH $SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.7-src.zip
ENV SPARK_OPTS --driver-java-options=-Xms1024M --driver-java-options=-Xmx4096M --driver-java-options=-Dlog4j.logLevel=info
ENV PATH=$SPARK_HOME/bin:$PATH
ENV PYSPARK_PYTHON=python3

ENV JAVA_HOME /usr/lib/jvm/java-1.8.0-openjdk-amd64/jre
ENV PATH $PATH:${JAVA_HOME}/bin:/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin 

# HADOOP installation
ENV HADOOP_VERSION 2.7.3
RUN wget --no-verbose https://archive.apache.org/dist/hadoop/core/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz && \
    tar -xvzf hadoop-${HADOOP_VERSION}.tar.gz  && \
    mv hadoop-${HADOOP_VERSION} /hadoop && \
    rm -rf /hadoop-${HADOOP_VERSION}.tar.gz
RUN mkdir -p /root/.ssh

RUN apt-get update && apt-get install -yq python3 openssh-server

# HADOOP & YARN config
ENV HADOOP_HOME /hadoop
ENV HADOOP_CONF_DIR ${HADOOP_HOME}/etc/hadoop
ENV HADOOP_HDFS_HOME ${HADOOP_HOME}
ENV YARN_HOME ${HADOOP_HOME}
ENV PATH $PATH:${HADOOP_HOME}/bin:${HADOOP_HOME}/sbin
ENV HADOOP_PREFIX ${HADOOP_HOME}  

COPY core-site.xml ${HADOOP_CONF_DIR}/core-site.xml
COPY yarn-site.xml ${HADOOP_CONF_DIR}/yarn-site.xml
COPY hdfs-site.xml ${HADOOP_CONF_DIR}/hdfs-site.xml
COPY slaves ${HADOOP_CONF_DIR}/slaves

# SSH config and launch
COPY ssh_config /etc/ssh/ssh_config
COPY ssh_config /root/.ssh/config
RUN chmod 600 /root/.ssh/config /etc/ssh/ssh_config && \
    chown root:root /root/.ssh/config /etc/ssh/ssh_config
RUN ssh-keygen -t rsa -P '' -f /root/.ssh/id_rsa && \
    cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys && \
    chmod 0600 ~/.ssh/authorized_keys && \
    service ssh start

# HIVE installation
ENV HIVE_VERSION 2.3.5
ENV HIVE_HOME /hive
ENV PATH $PATH:${HIVE_HOME}/bin
RUN wget --no-verbose https://www-us.apache.org/dist/hive/hive-${HIVE_VERSION}/apache-hive-${HIVE_VERSION}-bin.tar.gz && \   
    tar -xvzf apache-hive-${HIVE_VERSION}-bin.tar.gz  && \
    mv apache-hive-${HIVE_VERSION}-bin /hive && \
    rm -rf apache-hive-${HIVE_VERSION}-bin.tar.gz

# ALWAYS chmod +x shell scripts before COPY!
COPY start-yarn-master.sh /
COPY start-yarn-slave.sh /

EXPOSE 9000 50070 8020 50075 22 8022 8088 8040 8025 8030

# CMD "${HADOOP_HOME}/sbin/hadoop-daemon.sh --config ${HADOOP_CONF_DIR} --script hdfs start namenode"
CMD "/start-yarn-master.sh"
# CMD "nohup /start-yarn-master.sh &>/dev/null && bash"

# docker run -it --rm --name yarn-master -p 50070:50070 -p 9000:9000 -p 8020:8020 --hostname yarn-master --network yarn-cluster dataismus/yarn_node

# CMD "$HADOOP_HOME/sbin/hadoop-daemons.sh --config $HADOOP_CONF_DIR --script hdfs start datanode"

# CMD "$HADOOP_HOME/sbin/yarn-daemon.sh start resourcemanager"

# CMD "${HADOOP_HOME}/sbin/yarn-daemon.sh start nodemanager"

#########################################
#########################################