FROM ubuntu AS build

RUN apt-get update \
  && apt-get install -y gcc make unzip wget \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src

ARG CC65_VERSION=2.18

RUN wget https://github.com/cc65/cc65/archive/V${CC65_VERSION}.zip \
  && unzip V${CC65_VERSION}.zip \
  && cd cc65-${CC65_VERSION} \
  && export PREFIX=/opt/cc65 \
  && make \
  && make install \
  && strip $PREFIX/bin/*

FROM ubuntu

COPY --from=build /opt/cc65 /opt/cc65

ENV PATH /opt/cc65/bin:$PATH

WORKDIR /workdir
