FROM	ubuntu:16.04
MAINTAINER	Eugene <1@1.net>

ARG home=/
ENV home=$home

RUN	apt-get update && apt-get install -y wget build-essential pkg-config cmake unzip python python-zmq zlib1g-dev wget libcurl4-openssl-dev automake curl

RUN wget https://github.com/mochimodev/mochimo/raw/master/mochimo-main-net-v1.6.tgz
RUN tar zxvf mochimo-main-net-v1.6.tgz

WORKDIR /mochi/src
#RUN rm makeunx
#RUN wget http://orthoped.org/makeunx
#RUN chmod +x makeunx
RUN ./makeunx bin 
RUN ./makeunx install 
WORKDIR /mochi/bin 
RUN rm maddr.dat
RUN wget http://orthoped.org/maddr.dat


ENTRYPOINT ["/bin/bash", "-c", "/mochi/bin/./gomochi d"]
