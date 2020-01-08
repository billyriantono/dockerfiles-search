FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04

LABEL maintainer="huyu <huyu.sakuya4645@gmail.com>"

ENV PYTHON_VERSION 3.7.6

ENV DEBIAN_FRONTEND_OLD $DEBIAN_FRONTEND
ENV DEBIAN_FRONTEND noninteractive

ENV TZ Asia/Tokyo

# Python の依存関係パッケージを取得
RUN apt update  \
 && apt upgrade -y  \
 && apt install -y build-essential libbz2-dev libdb-dev \
                   libreadline-dev libffi-dev libgdbm-dev liblzma-dev \
                   libncursesw5-dev libsqlite3-dev libssl-dev \
                   zlib1g-dev uuid-dev tk-dev wget

# Python ソースコードの取得・展開
RUN wget -q https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz
RUN tar xzf Python-$PYTHON_VERSION.tgz

# Python ビルド
RUN cd Python-$PYTHON_VERSION \
 && ./configure --enable-shared \
 && make -j12 \
 && make install

# Python ソースコードの後始末
RUN rm -rf Python-$PYTHON_VERSION.tgz Python-$PYTHON_VERSION

# Python コマンドの設定
RUN export PYTHON_MAJOR_VERSION=$(echo $PYTHON_VERSION | cut -c 1) \
 && ln -s /usr/local/bin/python$PYTHON_MAJOR_VERSION /usr/local/bin/python \
 && ln -s /usr/local/bin/pip$PYTHON_MAJOR_VERSION    /usr/local/bin/pip
RUN echo "/usr/local/lib" > /etc/ld.so.conf.d/custom_python3.conf
RUN ldconfig

# 後始末
ENV DEBIAN_FRONTEND $DEBIAN_FRONTEND_OLD

ENTRYPOINT ["python"]
