FROM alpine:latest

ENV OPENJDK_VERSION=8 HADOOP_VERSION=2.9.1 MAHOUT_VERSION=0.13.0

WORKDIR /root

# change mirror source
RUN sed -i 's/http:\/\/dl-cdn.alpinelinux.org/https:\/\/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories

# install openssh-server, openjdk and wget
RUN apk --no-cache update && \
    apk --no-cache upgrade -vv && \
    apk --no-cache add -vv bash openssh openssh-server openjdk${OPENJDK_VERSION} && \
    rm -vrf /var/cache/apk/* && \
    rm -vrf /var/lib/apk/* && \
    rm -vrf /etc/apk/cache/*

# install Hadoop 2.9.1
RUN wget https://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz && \
    tar -vxzf hadoop-${HADOOP_VERSION}.tar.gz && \
    mkdir -v /opt && \
    mv -v hadoop-${HADOOP_VERSION} /opt/hadoop && \
    rm -vrf hadoop-${HADOOP_VERSION}.tar.gz

# install Mahout 0.13.0
RUN wget https://mirrors.tuna.tsinghua.edu.cn/apache/mahout/${MAHOUT_VERSION}/apache-mahout-distribution-${MAHOUT_VERSION}.tar.gz && \
    tar -vxzf apache-mahout-distribution-${MAHOUT_VERSION}.tar.gz && \
    mv -v apache-mahout-distribution-${MAHOUT_VERSION} /opt/mahout && \
    rm -vrf apache-mahout-distribution-${MAHOUT_VERSION}.tar.gz

# set environment variable
ENV JAVA_HOME=/usr/lib/jvm/java-1.${OPENJDK_VERSION}-openjdk
ENV HDFS_NAMENODE_SECURE_USER=root HDFS_DATANODE_SECURE_USER=root HDFS_SECONDARYNAMENODE_USER=root
ENV YARN_RESOURCEMANAGER_USER=root YARN_NODEMANAGER_USER=root
ENV HADOOP_HOME=/opt/hadoop
ENV HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
ENV HADOOP_COMMON_HOME=$HADOOP_HOME HADOOP_HDFS_HOME=$HADOOP_HOME HADOOP_MAPRED_HOME=$HADOOP_HOME HADOOP_YARN_HOME=$HADOOP_HOME 
ENV MAHOUT_HOME=/opt/mahout
ENV MAHOUT_HOME_CONF_DIR=$MAHOUT_HOME/conf
ENV PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$MAHOUT_HOME/conf:$MAHOUT_HOME/bin

# set SSH without key
RUN ssh-keygen -t rsa -f ~/.ssh/id_rsa -P '' && \
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

RUN mkdir -vp ~/hdfs/namenode && \ 
    mkdir -vp ~/hdfs/datanode && \
    mkdir -v $HADOOP_HOME/logs

COPY config/* /tmp/

RUN mv -v /tmp/ssh_config ~/.ssh/config && \
    mv -v /tmp/hadoop-env.sh $HADOOP_HOME/etc/hadoop/hadoop-env.sh && \
    mv -v /tmp/hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml && \ 
    mv -v /tmp/core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml && \
    mv -v /tmp/mapred-site.xml $HADOOP_HOME/etc/hadoop/mapred-site.xml && \
    mv -v /tmp/yarn-site.xml $HADOOP_HOME/etc/hadoop/yarn-site.xml && \
    mv -v /tmp/slaves $HADOOP_HOME/etc/hadoop/slaves && \
    mv -v /tmp/start-hadoop.sh ~/start-hadoop.sh && \
    mv -v /tmp/run-wordcount.sh ~/run-wordcount.sh && \
    mv -v /tmp/run-kmeans.sh ~/run-kmeans.sh && \
    sed -i "s/java-VERSION-openjdk/java-1.${OPENJDK_VERSION}-openjdk/g"  $HADOOP_HOME/etc/hadoop/hadoop-env.sh

RUN chmod +x ~/start-hadoop.sh && \
    chmod +x ~/run-wordcount.sh && \
    chmod +x ~/run-kmeans.sh && \
    chmod +x $HADOOP_HOME/sbin/start-dfs.sh && \
    chmod +x $HADOOP_HOME/sbin/start-yarn.sh 

# format namenode
RUN $HADOOP_HOME/bin/hdfs namenode -format

# generating key
RUN rm -vrf /etc/ssh/ssh*key && \
    ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N "" && \
    ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key -N "" && \
    ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key -N "" && \
    ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key -N ""

RUN echo "PS1='\[\033[01;32m\][\u@\h\[\033[01;37m\] \W\[\033[01;32m\]]\$\[\033[00m\] '" >> /etc/bash.bashrc