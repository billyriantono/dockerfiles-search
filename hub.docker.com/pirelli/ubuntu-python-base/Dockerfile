# Basic Python + Postgresql libs

FROM ubuntu:xenial
MAINTAINER Thomas Alisi <thomas.alisi.ex@pirelli.com>

ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive
ENV PYTHONUNBUFFERED 1

##################################
# basic ubuntu setup

RUN apt-get update -y && \
    apt-get install -y \
    software-properties-common \
    unattended-upgrades && \
    cp /usr/share/unattended-upgrades/20auto-upgrades /etc/apt/apt.conf.d/20auto-upgrades && \
    apt-get dist-upgrade -y

RUN apt-get install -y \
    build-essential \
    libreadline-gplv2-dev \
    libncursesw5-dev \
    libssl-dev \
    libsqlite3-dev \
    tk-dev libgdbm-dev \
    libc6-dev \
    libbz2-dev \
    zlib1g \
    zlib1g-dev \
    libaio-dev \
    openssl \
    ssh \
    ssh-client \
    git \
    htop \
    supervisor \
    wget \
    curl \
    unzip \
    nginx \
    python \
    python-setuptools \
    python-dev \
    python-pip \
    python-virtualenv

##################################
# forward nginx request and error to stdout (will be picked by docker + supervisor collectors)

RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

##################################
# install python3 from sources

RUN cd /tmp && \
    wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tgz && \
    tar xzf Python-3.6.1.tgz && \
    cd /tmp/Python-3.6.1 && \
    ./configure && make && make altinstall && \
    cd /root && \
    rm -rf /tmp/Python-3.6.1*

##################################
# basic database drivers

RUN apt-get install -y \
    unixodbc \
    unixodbc-dev \
    freetds-dev \
    freetds-bin \
    tdsodbc

##################################
# postgres 9.4 / 9.5 drivers on ubuntu 16.04

RUN sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' && \
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y libpq-dev && \
    apt-get clean

# full postgresql server, anyone? uncomment below if needed
# RUN apt-get install postgresql postgresql-contrib

##################################
# oracle driver

COPY /opt/oracle /tmp/oracle

RUN cd /tmp/oracle && \
    unzip instantclient-basic*.zip && \
    unzip instantclient-sdk*.zip && \
    rm instantclient-*.zip && \
    mkdir /opt/oracle && \
    mv instantclient_* /opt/oracle

ENV ORACLE_HOME /opt/oracle/instantclient_12_1

RUN echo "export ORACLE_HOME=/opt/oracle/instantclient_12_1" >> /etc/environment && \
    echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME" >> /etc/environment && \
    export ORACLE_HOME=/opt/oracle/instantclient_12_1 && \
    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME && \
    cd $ORACLE_HOME && \
    ln -s libclntsh.so.12.1 libclntsh.so && \
    echo "$ORACLE_HOME" >> /etc/ld.so.conf.d/oracle.conf && \
    ldconfig
    
##################################
# setup python 2 & 3 virtualenv 

RUN virtualenv /opt/venv2 && \
    python3.6 -m venv /opt/venv3

##################################
# install node from sources

RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - && \
    apt-get install -y nodejs && npm install npm@latest -g && \
    npm install -g gulp
