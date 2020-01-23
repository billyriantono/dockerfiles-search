#
# Brian LI's Developement Environment
#
FROM     ubuntu:14.04
MAINTAINER Brian LI <libiao@gmail.com>

# Last Package Update & Install
RUN apt-get update && \
        apt-get install -y --no-install-recommends  && \
        apt-get install -y  build-essential autoconf automake gcc g++ python ruby gettext libncurses5-dev libacl1-dev  libperl-dev python-dev libgcrypt11-dev pkg-config  zlib1g-dev  && \
        apt-get install -y wget curl supervisor openssh-server net-tools iputils-ping nano vim  make ctags cscope git mercurial subversion aptitude  && \
        apt-get install -y lrzsz zip unzip p7zip-full sysstat && \
        apt-get install -y dnsmasq network-manager && \
        apt-get -y autoremove && \
        apt-get  -y autoclean && \
        apt-get -y clean && \
        rm -rf /var/lib/apt/lists/*

# Install all to /opt/*
ENV OPT_DIR /opt

# Timezone
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Java
ENV JAVA_HOME /opt/jdk
ENV PATH $PATH:$JAVA_HOME/bin
RUN cd $OPT_DIR \
    && curl -SL -k "http://download.oracle.com/otn-pub/java/jdk/8u66-b17/jdk-8u66-linux-x64.tar.gz" -b "oraclelicense=a" \
    |  tar xz \
    && ln -s /opt/jdk1.8.0_66 /opt/jdk \
    && rm -f /opt/jdk/*src.zip \
    && echo '' >> /etc/profile \
    && echo '# JDK' >> /etc/profile \
    && echo "export JAVA_HOME=$JAVA_HOME" >> /etc/profile \
    && echo 'export PATH="$PATH:$JAVA_HOME/bin"' >> /etc/profile \
    && echo '' >> /etc/profile

# Hadoop
ENV HADOOP_URL http://www.eu.apache.org/dist/hadoop/common
ENV HADOOP_VERSION 2.7.1
RUN cd $OPT_DIR \
    && curl -SL -k "$HADOOP_URL/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz" \
    |  tar xz \
    && ln -s /opt/hadoop-$HADOOP_VERSION /opt/hadoop \
    && rm -Rf /opt/hadoop/share/doc

ENV HADOOP_PREFIX $OPT_DIR/hadoop
ENV PATH $PATH:$HADOOP_PREFIX/bin:$HADOOP_PREFIX/sbin
ENV HADOOP_MAPRED_HOME $HADOOP_PREFIX
ENV HADOOP_COMMON_HOME $HADOOP_PREFIX
ENV HADOOP_HDFS_HOME $HADOOP_PREFIX
ENV YARN_HOME $HADOOP_PREFIX
RUN echo '# Hadoop' >> /etc/profile \
    && echo "export HADOOP_PREFIX=$HADOOP_PREFIX" >> /etc/profile \
    && echo 'export PATH=$PATH:$HADOOP_PREFIX/bin:$HADOOP_PREFIX/sbin' >> /etc/profile \
    && echo 'export HADOOP_MAPRED_HOME=$HADOOP_PREFIX' >> /etc/profile \
    && echo 'export HADOOP_COMMON_HOME=$HADOOP_PREFIX' >> /etc/profile \
    && echo 'export HADOOP_HDFS_HOME=$HADOOP_PREFIX' >> /etc/profile \
    && echo 'export YARN_HOME=$HADOOP_PREFIX' >> /etc/profile

# Add in the etc/hadoop directory
ADD conf/core-site.xml $HADOOP_PREFIX/etc/hadoop/core-site.xml
ADD conf/hdfs-site.xml $HADOOP_PREFIX/etc/hadoop/hdfs-site.xml
ADD conf/yarn-site.xml $HADOOP_PREFIX/etc/hadoop/yarn-site.xml
ADD conf/mapred-site.xml $HADOOP_PREFIX/etc/hadoop/mapred-site.xml
RUN sed -i '/^export JAVA_HOME/ s:.*:export JAVA_HOME=/opt/jdk:' $HADOOP_PREFIX/etc/hadoop/hadoop-env.sh

# Name node foramt
RUN hdfs namenode -format

# Scala
ENV SCALA_HOME /opt/scala
ENV SCALA_VERSION 2.11.8
RUN cd $OPT_DIR \
    && curl -SL -k "http://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz" \
    | tar xz \
    && rm -f scala-$SCALA_VERSION.tgz \
    && ln -s scala-$SCALA_VERSION scala \
    && echo '' >> /etc/profile \
    && echo '# SCALA' >> /etc/profile \
    && echo "export SCALA_HOME=$SCALA_HOME" >> /etc/profile \
    && echo 'export PATH="$PATH:$SCALA_HOME/bin"' >> /etc/profile \
    && echo '' >> /etc/profile

# Spark
ENV SPARK_HOME /opt/spark
RUN cd $OPT_DIR \
    && curl -SL -k "http://d3kbcqa49mib13.cloudfront.net/spark-2.0.0-bin-hadoop2.7.tgz" \
    | tar xz \
    && rm -f spark-2.0.0-bin-hadoop2.7.tgz \
    && ln -s spark-2.0.0-bin-hadoop2.7 spark \
    && echo '' >> /etc/profile \
    && echo '# SPARK' >> /etc/profile \
    && echo "export SPARK_HOME=$SPARK_HOME" >> /etc/profile \
    && echo 'export PATH="$PATH:$SPARK_HOME/bin"' >> /etc/profile \
    && echo '' >> /etc/profile

#Zookeeper
ENV ZK_VERSION 3.4.8
ENV ZK_HOME /opt/zookeeper
RUN cd $OPT_DIR \
     && curl -SL -k http://www-us.apache.org/dist/zookeeper/zookeeper-$ZK_VERSION/zookeeper-$ZK_VERSION.tar.gz | tar xz \
     &&  rm -f zookeeper-$ZK_VERSION.tar.gz \
     &&  ln -s zookeeper-$ZK_VERSION zookeeper  && \
     echo '' >> /etc/profile && \
     echo '# Zookeeper ' >> /etc/profile && \
     echo "export ZOOKEEPER_HOME=$ZK_HOME" >> /etc/profile && \
     echo 'export PATH="$PATH:$ZK_HOME/bin"' >> /etc/profile && \
     echo '' >> /etc/profile

RUN mv $ZK_HOME/conf/zoo_sample.cfg $ZK_HOME/conf/zoo.cfg
RUN mkdir /tmp/zookeeper

# HBase configuration
ENV HBASE_HOME /opt/hbase
ENV HBASE_VERSION 1.2.2
RUN cd $OPT_DIR && \
     curl -SL -k http://archive.apache.org/dist/hbase/$HBASE_VERSION/hbase-$HBASE_VERSION-bin.tar.gz | tar xz && \
     rm -f hbase-$HBASE_VERSION-bin.tar.gz && \
     ln -s hbase-$HBASE_VERSION hbase && \
     echo '' >> /etc/profile && \
     echo '# HBase' >> /etc/profile && \
     echo "export HBASE_HOME=$HBASE_HOME" >> /etc/profile && \
     echo 'export PATH="$PATH:$HBASE_HOME/bin"' >> /etc/profile && \
     echo '' >> /etc/profile

RUN sed -i "s,^. export JAVA_HOME.*,export JAVA_HOME=/opt/jdk," $HBASE_HOME/conf/hbase-env.sh
RUN rm $HBASE_HOME/conf/hbase-site.xml
ADD conf/hbase-site.xml $HBASE_HOME/conf/hbase-site.xml

# Vim configuration
ADD conf/vim/.vimrc /root/.vimrc
ADD conf/vim/.vim_csindent.ini /root/.vim_csindent.ini
COPY conf/vim/.vim /root/.vim

# Bazel configuration
RUN cd $OPT_DIR && \
     wget "https://github.com/bazelbuild/bazel/releases/download/0.3.1/bazel-0.3.1-installer-linux-x86_64.sh" && \
     chmod +x bazel-0.3.1-installer-linux-x86_64.sh && \
     ./bazel-0.3.1-installer-linux-x86_64.sh --user && \
     rm -f bazel-0.3.1-installer-linux-x86_64.sh && \
     echo 'export PATH="$PATH:$HOME/bin"' >> /etc/profile

# SSH keygen
RUN cd /root && ssh-keygen -t dsa -P '' -f "/root/.ssh/id_dsa" \
    && cat /root/.ssh/id_dsa.pub >> /root/.ssh/authorized_keys \
    && chmod 644 /root/.ssh/authorized_keys 

# Daemon supervisord
RUN mkdir -p /var/log/supervisor
ADD conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Daemon SSH 
RUN mkdir /var/run/sshd \
    && sed -i 's/without-password/yes/g' /etc/ssh/sshd_config \
    && sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config \
    && echo '    StrictHostKeyChecking no' >> /etc/ssh/ssh_config \
    && echo 'SSHD: ALL' >> /etc/hosts.allow

# Root password
RUN echo 'root:hadoop' | chpasswd

# Port
# Node Manager: 8042, Resource Manager: 8088, NameNode: 50070, DataNode: 50075, SecondaryNode: 50090, 
EXPOSE 22 8042 8088 50070 50075 50090

# Spark UI: 4040
EXPOSE 4040

# HBase REST API: 8080, HBase REST Web UI: 8085, HBase Thrift API: 9090, HBase Thrift Web UI: 9095, ZK Port: 2181, HBase Master web UI: 16010
EXPOSE 8080 8085 9090 9095 2181 16010

# Daemon
CMD ["/usr/bin/supervisord"]