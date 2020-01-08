FROM centos:6

MAINTAINER Tatsuhiko Kono<i@p-nitrite.net>

RUN yum update -y
RUN yum install which git python-setuptools -y
RUN cat /etc/ssh/ssh_config | sed -e 's/#   StrictHostKeyChecking ask/    StrictHostKeyChecking no/g' > /etc/ssh/ssh_config
RUN yum install gcc gcc-java libgcj libgcj-devel gcc-c++ wget unzip python-devel libjpeg-devel tar xz readline-devel sqlite-devel zlib-devel openssl-devel -y
WORKDIR /tmp
RUN wget https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tar.xz && tar xvf Python-2.7.11.tar.xz && cd /tmp/Python-2.7.11 && \
    ./configure --prefix=/usr/local && make && make install
    RUN cd /tmp && wget https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py && python ez_setup.py && easy_install pip

