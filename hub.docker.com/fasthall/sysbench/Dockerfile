FROM ubuntu:xenial

LABEL maintainer="weitsung@google.com,jiayingz@google.com"

RUN apt update && \
  apt install -y \
  git \
  make \
  automake \
  libtool \
  pkg-config \
  libaio-dev \
  libmysqlclient-dev \
  libssl-dev \
  libpq-dev

RUN git clone https://github.com/akopytov/sysbench.git

WORKDIR /sysbench

RUN ./autogen.sh
RUN CFLAGS=-g ./configure
RUN make -j
RUN make install

CMD ["bash"]
