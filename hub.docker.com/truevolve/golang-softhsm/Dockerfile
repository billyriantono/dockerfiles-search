FROM golang:1.7.6
MAINTAINER Stephen Hohls "steve@truevolve.technology"

USER root
RUN apt-get update && apt-get install -y build-essential autotools-dev libssl-dev dh-autoreconf libltdl-dev opensc opensc-pkcs11
RUN apt-get clean
RUN apt-get purge

RUN mkdir -p /src/softhsm2/
COPY SoftHSMv2-2.2.0.tar.gz /src/softhsm2.tag.gz
RUN tar xvf /src/softhsm2.tag.gz -C /src/softhsm2/ --strip-components=1
RUN cd /src/softhsm2/ && sh ./autogen.sh && ./configure && make && make install

RUN rm -rf /src

CMD bash
