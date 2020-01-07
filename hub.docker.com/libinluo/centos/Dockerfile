FROM centos:7.1.1503

RUN yum -y update \
    && yum -y install epel-release \
    && yum -y install gcc make git tar mariadb-devel libffi-devel openssl-devel \
    && yum -y clean all


RUN localedef -c -f UTF-8 -i en_US en_US.UTF-8 \
    && export LANG=en_US.UTF-8 \
    && export LC_ALL=en_US.UTF-8 \
    && rm -f /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime


ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
