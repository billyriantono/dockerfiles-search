FROM centos:6.9

MAINTAINER takamiiiii

RUN yum -y update
RUN yum -y groupinstall "Development Tools"

RUN yum -y install \
           kernel-devel \
           kernel-headers \
           gcc-c++ \
           patch \
           libyaml-devel \
           libffi-devel \
           autoconf \
           automake \
           make \
           libtool \
           bison \
           tk-devel \
           zip \
           wget \
           tar \
           gcc \
           zlib \
           zlib-devel \
           bzip2 \
           bzip2-devel \
           readline \
           readline-devel \
           sqlite \
           sqlite-devel \
           openssl \
           openssl-devel \
           git \
           gdbm-devel \
           python-devel



WORKDIR /root
RUN wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz \
        && tar zxf Python-3.6.5.tgz \
        && cd Python-3.6.5 \
        && ./configure \
        && make install


        RUN wget https://bootstrap.pypa.io/get-pip.py
        RUN python3.6 get-pip.py

COPY ./requirements.txt ./requirements.txt
RUN pip install -r requirements.txt



CMD ["/bin/bash"]
