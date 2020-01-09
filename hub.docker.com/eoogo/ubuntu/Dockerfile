FROM ubuntu
WORKDIR /root/
COPY apt/sources.list /etc/apt/
USER root
CMD '/bin/bash'
ENV TZ Asia/Shanghai
ENV LC_CTYPE zh_CN.UTF-8
ENV DEBIAN_FRONTEND noninteractive
RUN apt update && apt upgrade -y && \
    apt install -y language-pack-zh-hans lrzsz git python3 net-tools zip unzip unar curl wget vim sudo make && \
    echo 'set encoding=utf-8' >> /root/.vimrc
