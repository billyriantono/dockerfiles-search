FROM python:3.6

MAINTAINER Alex Myasoedov <msoedov@gmail.com>

ENV WORKDIR  /pyflame/
WORKDIR $WORKDIR
RUN apt-get update
RUN apt-get install autoconf automake autotools-dev g++ pkg-config python-dev python3-dev libtool make -y
RUN git clone https://github.com/uber/pyflame.git .
RUN ./autogen.sh
RUN ./configure
RUN make
RUN make install
RUN rm -rf $WORKDIR
COPY flamegraph.pl /usr/local/bin
