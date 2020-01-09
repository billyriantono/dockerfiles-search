FROM ubuntu:18.04
LABEL maintainer="feli5@cisco.com"

RUN apt-get update \
    && apt-get --assume-yes install iputils-ping net-tools git git-review \
        tox vim wget gcc g++ make libssl-dev curl zlib1g-dev libbz2-dev

RUN version=2.7.16 \
    && curl -LO https://www.python.org/ftp/python/${version}/Python-${version}.tgz \
    && tar zxf Python-${version}.tgz \
    && cd Python-${version} \
    && ./configure --with-zlib --prefix=$HOME/.Python-${version} \
    && make && make install \
    && virtualenv $HOME/.py27 -p $HOME/.Python-${version}/bin/python2.7 \
    && cd .. \
    && rm -f Python-${version}.tgz && rm -rf Python-${version} \
    && unset v

