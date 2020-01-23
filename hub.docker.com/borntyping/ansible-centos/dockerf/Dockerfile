FROM debian:buster-slim

RUN apt-get update && apt-get install -y curl wget unzip gzip xz-utils git \
  build-essential autoconf automake pkg-config libglib2.0-dev libtool \
  python3-dev python3-pip && \
  apt-get clean

# TODO: add openjdk-11-jdk-headless

WORKDIR /tmp
RUN wget https://github.com/lcm-proj/lcm/releases/download/v1.3.1/lcm-1.3.1.zip \
  && unzip lcm-1.3.1.zip && cd lcm-1.3.1 \
  && autoreconf -fi && ./configure && make && make install \
  && ldconfig \
  && ln -s /usr/local/lib/python3.7/site-packages/lcm /usr/local/lib/python3.7/dist-packages/ \
  && cd /tmp && rm -rvf lcm-1.3.1 && rm -v lcm-1.3.1.zip
