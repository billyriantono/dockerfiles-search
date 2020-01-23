FROM ubuntu:18.04
LABEL maintainer="daoying007 <daoying007@gmail.com>"
LABEL maintainer_eth_address="0xC53D71abA6C29F284836d76Df75a4967Cd96acf9"
LABEL github="https://github.com/daoying007/ckb-miner-docker"

USER root
RUN apt-get update
RUN apt-get install -y supervisor tzdata curl \
    && cp /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime

ARG MINER_VERSION="0.18.0"
ARG MINER_FILENAME="ckb_v${MINER_VERSION}_x86_64-unknown-linux-gnu.tar.gz"
ARG MINER_DIR="ckb_v${MINER_VERSION}_x86_64-unknown-linux-gnu"
ARG MINER_DOWNLOAD_URL="https://github.com/nervosnetwork/ckb/releases/download/v${MINER_VERSION}/${MINER_FILENAME}"

WORKDIR /var/lib

# 本地编译时下载github文件比较慢，提前下载好直接拷贝，提高容器编译速度
# ADD tmp/files /var/lib/
# 正式编译时通过github下载安装包再编译
RUN curl -fSL ${MINER_DOWNLOAD_URL} -o ${MINER_FILENAME}

RUN tar -xzvf ${MINER_FILENAME} \
    && mv ${MINER_DIR} ckb \
    && mkdir /var/lib/ckb/data
ADD etc/supervisor /etc/supervisor/
ADD scripts /root/
RUN chmod +x /root/*
WORKDIR /var/lib/ckb
RUN ln -snf "$(pwd)/ckb" /usr/local/bin/ckb \
    && ln -snf "$(pwd)/ckb-cli" /usr/local/bin/ckb-cli
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
