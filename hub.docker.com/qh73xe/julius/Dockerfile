# =============================================
# The Docker file for Julius
# =============================================
FROM ubuntu:artful
MAINTAINER qh73xe

# apt-get の最新化及びロケーション設定
# =============================================
RUN apt-get update && apt-get install -y locales && apt-get install -y language-pack-ja-base language-pack-ja && rm -rf /var/lib/apt/lists/* \
    && localedef -i ja_JP -c -f UTF-8 -A /usr/share/locale/locale.alias ja_JP.UTF-8
ENV LANG=ja_JP.UTF-8

# Julius 依存ライブラリのインストール
RUN apt-get update && apt-get install -yq \
    build-essential wget zlib1g-dev flex libasound2-dev libesd0-dev libsndfile1-dev \
    git git-lfs sox pulseaudio socat alsa-utils

# Julius ソースコードの取得
ENV JULIUS_VERSION=4.4.2
RUN wget https://github.com/julius-speech/julius/archive/v$JULIUS_VERSION.tar.gz -O "/tmp/julius.tar.gz"
RUN tar -xvzf "/tmp/julius.tar.gz" -C /usr/local/src && rm "/tmp/julius.tar.gz" 
RUN cd "/usr/local/src/julius-$JULIUS_VERSION" && CFLAGS='-O3' ./configure && make && make install
RUN git clone https://github.com/julius-speech/dictation-kit.git && \
    cd dictation-kit && git lfs pull

# python 環境の構築
RUN apt-get update && apt-get install -yq \
    python3 python3-pip

# python 環境
# =============================================
RUN pip3 install tornado

# 実行環境のコピー
COPY src /usr/src 
COPY misc /tmp/misc

# 音声認識サーバーとして起動
EXPOSE 8888
CMD ["python3", "/usr/src/server.py"]
