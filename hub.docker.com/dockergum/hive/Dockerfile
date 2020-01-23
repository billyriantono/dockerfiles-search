FROM dockergum/centos:jdk8

# version
ENV  HADOOP_VERSION 3.1.2
ENV  HIVE_VERSION   3.1.2

# common
ENV MULTIHOMED_NETWORK=1
ENV USER=root

# hadoop
ENV HADOOP_HOME     /opt/hadoop-$HADOOP_VERSION
ENV HADOOP_CONF_DIR /etc/hadoop
ENV PATH            $HADOOP_HOME/bin/:$PATH

# hive
ENV HIVE_HOME /opt/hive-$HIVE_VERSION
ENV PATH      $HIVE_HOME/bin:$PATH

# Install hadoop
RUN curl -fSL https://www.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz -o /tmp/hadoop.tar.gz && \
    tar -xvf /tmp/hadoop.tar.gz -C /opt/ && \
    rm -rf /tmp/* && \
    ln -s /opt/hadoop-$HADOOP_VERSION/etc/hadoop /etc/hadoop

# Install Hive and PostgreSQL JDBC
RUN curl -fSL https://archive.apache.org/dist/hive/hive-$HIVE_VERSION/apache-hive-$HIVE_VERSION-bin.tar.gz -o /tmp/apache-hive-$HIVE_VERSION-bin.tar.gz && \
    tar -xzvf /tmp/apache-hive-$HIVE_VERSION-bin.tar.gz -C /opt/ && \
    mv /opt/apache-hive-$HIVE_VERSION-bin /opt/hive-$HIVE_VERSION && \
    curl -fSL https://jdbc.postgresql.org/download/postgresql-9.4.1212.jar -o $HIVE_HOME/lib/postgresql-jdbc.jar && \
    rm -rf /tmp/* && \
    ln -s $HIVE_HOME/conf /etc/hive

ENTRYPOINT ["sleep"]
CMD ["infinity"]
