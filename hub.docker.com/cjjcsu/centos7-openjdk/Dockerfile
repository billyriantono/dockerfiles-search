FROM centos:7.2.1511

# cjjcsu/centos7-openjdk:1.0
MAINTAINER cjjcsu <cjjcsu@outlook.com>

WORKDIR /opt

# install tools & install jdk & clean package
RUN yum install openssh-server \ 
    openssh-clients \
    initscripts \
    rsync \
    curl \
    telnet \
    wget \
    vim \
    java-1.8.0-openjdk-devel.x86_64 -y \ 
    && yum clean all \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/shanghai" > /etc/timezone \
    && ulimit -n 10240

# ssh without key
ADD ssh-config /root/.ssh/config
RUN chmod 600 /root/.ssh/config && \
    chown root:root /root/.ssh/config && \
    echo "/usr/sbin/sshd" >> ~/.bashrc && \
    ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa && \
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
    /usr/bin/ssh-keygen -A