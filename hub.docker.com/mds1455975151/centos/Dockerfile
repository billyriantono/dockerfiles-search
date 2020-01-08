FROM centos:7

MAINTAINER Ma DongSheng <mdscdpc@gmail.com>

COPY Centos-7.repo epel-7.repo /etc/yum.repos.d/

RUN sed -i.backup 's/^enabled=1/enabled=0/' /etc/yum/pluginconf.d/fastestmirror.conf && \
    yum install -y gcc gcc-c++ automake autoconf tree telnet python-pip python-devel && \
    pip install --upgrade pip

CMD ["/bin/bash"]
