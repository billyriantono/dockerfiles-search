FROM amazonlinux:2017.09
MAINTAINER Mandus Momberg

RUN yum -y install \
    python27 \
    python27-devel \
    python27-pip \
    zip \
    gcc \
    gcc-c++ \
    make \
    openssl-devel

RUN curl -kLo /tmp/node-v6.12.0.tar.gz  "https://nodejs.org/dist/latest-v6.x/node-v6.12.0.tar.gz" \
  && tar -xf /tmp/node-v6.12.0.tar.gz -C /tmp

WORKDIR /tmp/node-v6.12.0

RUN ./configure \
  && make -j4 \
  && make install
