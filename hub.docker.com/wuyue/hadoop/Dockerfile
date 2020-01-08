FROM centos:7
RUN yum install -y sudo wget which java-11-openjdk java-11-openjdk-devel net-tools
RUN groupadd --gid 1000 hadoop
RUN useradd --uid 1000 hadoop --gid 100 --home /opt/hadoop
RUN chmod 755 /opt/hadoop
RUN echo "hadoop ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
ENV HADOOP_VERSION=3.2.1
ENV JAVA_HOME=/usr/lib/jvm/jre/
ENV HADOOP_HOME=/opt/hadoop
ENV PATH $PATH:$HADOOP_HOME/bin

# add scripts
ADD scripts/start-node.py /opt/
ADD scripts/run-wordcount.sh /opt/

RUN chown hadoop:users /opt

RUN mkdir -p /data/hdfs/{namenode,datanode}
RUN chown -R hadoop:users /data
RUN mkdir -p /var/log/hadoop && chmod 1777 /var/log/hadoop
ENV HADOOP_LOG_DIR=/var/log/hadoop
ENV HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
WORKDIR /opt/hadoop
USER hadoop
ARG HADOOP_URL=https://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz
WORKDIR /opt
RUN sudo rm -rf /opt/hadoop && wget $HADOOP_URL -O hadoop.tar.gz && tar zxf hadoop.tar.gz && rm hadoop.tar.gz && mv hadoop* hadoop && rm -rf /opt/hadoop/share/doc
WORKDIR /opt/hadoop

CMD ["python" ,"/opt/start-node.py"]