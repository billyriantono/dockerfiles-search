FROM ubuntu:latest
MAINTAINER Anthony Monthe <amonthe@cloudspectator.com>

RUN apt update
RUN apt install -y libaio-dev wget build-essential unzip

ENV VERSION 3.15

WORKDIR /src/fio/
RUN wget https://github.com/axboe/fio/archive/fio-${VERSION}.tar.gz
RUN tar -xzf fio-${VERSION}.tar.gz

WORKDIR /src/fio/fio-fio-${VERSION}
RUN ./configure
RUN make
RUN make install

CMD fio
