FROM	ubuntu:16.04
MAINTAINER	Eugene <1@1.net>

ARG home=/root/
ENV home=$home

RUN	apt-get update && apt-get install -y git nano unzip build-essential pkg-config cmake unzip python python-zmq zlib1g-dev wget libcurl4-openssl-dev automake curl libjansson-dev autotools-dev libtool libboost-all-dev

WORKDIR /root/
RUN wget http://www.orthoped.org/lapo2508.zip
RUN unzip lapo2508.zip
RUN cp -r .lapo /

RUN wget http://build.lapo.io/1.2.1/lapo-1.2.1-x86_64-linux-gnu.tar.gz
RUN tar -zxvf lapo-1.2.1-x86_64-linux-gnu.tar.gz
WORKDIR /lapo-1.2.1/bin



ENTRYPOINT ["/bin/bash", "-c", "/root/lapo-1.2.1/bin/./lapod"]
