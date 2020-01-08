FROM cjjcsu/centos7-openjdk:8

MAINTAINER cjjcsu <cjjcsu@outlook.com>

WORKDIR /opt

ENV HADOOP_VERSION=2.9.1

# install openssh-server
RUN rpm --rebuilddb && yum install -y python-setuptools openssh-server && easy_install supervisor && yum clean all

# install hadoop
RUN curl -O http://mirrors.tuna.tsinghua.edu.cn/apache/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz && \
    tar -xzvf hadoop-${HADOOP_VERSION}.tar.gz && \
    mv hadoop-${HADOOP_VERSION} /usr/local/hadoop && \
    rm hadoop-${HADOOP_VERSION}.tar.gz

# set environment variable
ENV HADOOP_HOME=/usr/local/hadoop
ENV PATH=$PATH:/usr/local/hadoop/bin:/usr/local/hadoop/sbin

# ssh without key
RUN ssh-keygen -t rsa -f ~/.ssh/id_rsa -P '' && \
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
    echo "StrictHostKeyChecking no" > /etc/ssh/ssh_config
    # sed -i "s/#   StrictHostKeyChecking ask/StrictHostKeyChecking no/g" /etc/ssh/ssh_config