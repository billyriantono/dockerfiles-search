FROM dockergum/centos:jdk8

# version
ENV HADOOP_VERSION 3.1.2

# common
ENV MULTIHOMED_NETWORK=1
ENV USER=root

# hadoop
ENV HADOOP_HOME     /opt/hadoop-$HADOOP_VERSION
ENV HADOOP_CONF_DIR /etc/hadoop
ENV PATH            $HADOOP_HOME/bin/:$PATH

# Install hadoop
ENV HADOOP_URL https://www.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz

RUN curl -fSL "$HADOOP_URL" -o /tmp/hadoop.tar.gz && \
    tar -xvf /tmp/hadoop.tar.gz -C /opt/ && \
    rm -rf /tmp/* && \
    ln -s /opt/hadoop-$HADOOP_VERSION/etc/hadoop /etc/hadoop


ENTRYPOINT ["sleep"]
CMD ["infinity"]
