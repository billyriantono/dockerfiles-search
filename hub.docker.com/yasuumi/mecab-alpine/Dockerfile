FROM alpine

ENV MECAB_VERSION 0.996
ENV MECAB_URL https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7cENtOXlicTFaRUE
ENV IPADIC_VERSION 2.7.0-20070801
ENV IPADIC_URL https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7MWVlSDBCSXZMTXM

RUN apk add --no-cache --virtual .builddeps\
    curl make g++ file bash openssl git && \
    # install mecab
    mkdir /temp && cd /temp && \
    curl -SL -o mecab-${MECAB_VERSION}.tar.gz ${MECAB_URL} && \
    tar zxf mecab-${MECAB_VERSION}.tar.gz && \
    cd mecab-${MECAB_VERSION} && \
    ./configure --enable-utf8-only --with-charset=utf8 && \
    make && make install && ldconfig /usr/local/lib && \
    cd && rm -r /temp && \
    # install mecab-ipadic
    mkdir /temp && cd /temp && \
    curl -SL -o mecab-ipadic-${IPADIC_VERSION}.tar.gz ${IPADIC_URL} && \
    tar zxf mecab-ipadic-${IPADIC_VERSION}.tar.gz && \
    cd mecab-ipadic-${IPADIC_VERSION} && \
    ./configure --with-charset=utf8 && \
    make && make install && \
    cd && rm -rf /temp && \
    # install mecab-ipadic-neologd
    mkdir /temp && cd /temp && \
    git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git && \
    mecab-ipadic-neologd/bin/install-mecab-ipadic-neologd -n -y && \
    cd && rm -rf /temp && \
    # remove dependencies
    apk del --purge .builddeps