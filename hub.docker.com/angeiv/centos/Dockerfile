FROM angeiv/centos:7
MAINTAINER Angeiv Zhang <angeiv.zhang@gmail.com>

RUN yum makecache fast \
    && yum -y upgrade \
    && yum install -y gem \
    ruby-devel \
    zlib-devel \
    git \
    make \
    gcc \
    gcc-c++ \
    && yum clean all \
    && echo "        StrictHostKeyChecking no" >> /etc/ssh/ssh_config \
    && echo "        UserKnownHostsFile /dev/null" >> /etc/ssh/ssh_config

RUN gem install bundler

CMD ["/bin/bash"]
