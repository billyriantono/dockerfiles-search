FROM ubuntu:16.04

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y ca-certificates wget apt-transport-https vim python-setuptools lsb-release && \
    apt-get clean

RUN apt-get install -y build-essential checkinstall libreadline-gplv2-dev \
    libncursesw5-dev libssl-dev libsqlite3-dev libgdbm-dev libc6-dev \
    libbz2-dev openssl

RUN cd /tmp && wget https://www.python.org/ftp/python/3.4.5/Python-3.4.5.tgz && tar zxf Python-3.4.5.tgz && \
    cd Python-3.4.5 && ./configure --enable-shared --prefix=/usr/local LDFLAGS="-Wl,--rpath=/usr/local/lib" && \
    make altinstall

RUN easy_install pip
RUN pip install virtualenv
RUN pip install tox
RUN pip install radon

RUN apt-get -y install openssh-client git

RUN rm -rf /var/lib/apt/lists/*
RUN rm -rf /var/cache/apt/archives/*
