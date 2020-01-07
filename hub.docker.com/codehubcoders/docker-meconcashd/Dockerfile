FROM ubuntu:xenial

RUN apt-get update -qq
RUN apt-get upgrade -y -qq
RUN apt-get install -y -qq \
    wget \
    autoconf \
    build-essential \
    pkg-config \
    libssl-dev \
    libboost-all-dev \
    miniupnpc \
    libminiupnpc-dev \
    gettext

ENV MECONCASH_VERSION 0.8.7

RUN wget -q https://github.com/mecon-coin/meconcash-core/archive/${MECONCASH_VERSION}.tar.gz
RUN tar -xzf *.tar.gz
RUN rm -rf ${MECONCASH_VERSION}.tar.gz

WORKDIR /meconcash-core-${MECONCASH_VERSION}

RUN ./contrib/install_db4.sh `pwd`
RUN ln -sf `pwd`/db4/include /usr/local/include/bdb4.8
RUN ln -sf `pwd`/db4/lib/*.a /usr/local/lib
RUN ./autogen.sh
RUN ./configure \
    --disable-tests \
    --disable-ccache \
    --with-gui=no

RUN find . -name '*.sh' -type f | xargs chmod +x

RUN make -j$(nproc)

RUN cp src/meconcashd /bin
RUN cp src/meconcash-cli /bin
RUN mkdir -p /root/.meconcash

COPY meconcash.conf /root/.meconcash/meconcash.conf

VOLUME ["/root/.meconcash"]

EXPOSE 29901 29902

CMD ["meconcashd"]