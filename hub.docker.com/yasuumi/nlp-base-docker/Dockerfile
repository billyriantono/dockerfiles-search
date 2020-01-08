FROM ubuntu:16.04
MAINTAINER "Yasuumi Nishikawa" <yasu.umi.19910101@gmail.com>

ENV MECAB_VERSION 0.996
ENV MECAB_URL https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7cENtOXlicTFaRUE
ENV IPADIC_VERSION 2.7.0-20070801
ENV IPADIC_URL https://drive.google.com/uc?export=download&id=0B4y35FiV1wh7MWVlSDBCSXZMTXM
ENV TENSORFLOW_URL https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.8.0-cp27-none-linux_x86_64.whl

RUN apt-get update && apt-get upgrade -qy && \
    apt-get install -y --no-install-recommends \
    curl git file build-essential pkg-config \
    libblas-dev liblapack-dev libatlas-base-dev gfortran \
    libfreetype6-dev libpng-dev \
    libmysqlclient-dev libffi-dev libssl-dev lib32ncurses5-dev libhdf5-dev cython \
    python-dev python-pip && \
    apt-get clean && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/* && \

# install mecab
    mkdir /temp && cd /temp && \
    curl -SL -o mecab-${MECAB_VERSION}.tar.gz ${MECAB_URL} && \
    tar zxf mecab-${MECAB_VERSION}.tar.gz && \
    cd mecab-${MECAB_VERSION} && \
    ./configure --enable-utf8-only --with-charset=utf8 && \
    make && make install && ldconfig && \
    cd && rm -r /temp && \

# install mecab-ipadic
    mkdir /temp && cd /temp && \
    curl -SL -o mecab-ipadic-${IPADIC_VERSION}.tar.gz ${IPADIC_URL} && \
    tar zxf mecab-ipadic-${IPADIC_VERSION}.tar.gz && \
    cd mecab-ipadic-${IPADIC_VERSION} && \
    ./configure --with-charset=utf8 && \
    make && make install && \
    cd && rm -rf /temp && \

# install tensorflow
    pip install pip --ignore-installed --upgrade && \
    pip install --ignore-installed --upgrade ${TENSORFLOW_URL} && \

# install mecab-ipadic-neologd
    mkdir /temp && cd /temp && \
    git clone --depth 1 https://github.com/neologd/mecab-ipadic-neologd.git && \
    mecab-ipadic-neologd/bin/install-mecab-ipadic-neologd -n -y && \
    cd && rm -rf /temp

CMD ["/bin/bash"]
