FROM ubuntu:latest


WORKDIR /opt/sumokoin

RUN set -ex && \
    apt -qq update && \
    apt -qq install wget -y && \
    wget -qO /tmp/sumokoin.tar.bz2 https://github.com/sumoprojects/sumokoin/releases/download/v0.5.1.0/sumokoin.linux.x64.v0-5-1-0.tar.bz2 && \
    tar jxf /tmp/sumokoin.tar.bz2 && \
    rm /tmp/sumokoin.tar.bz2 && \
    mv /opt/sumokoin/sumokoin.linux.x64.v0-5-1-0/sumo-wallet-rpc /opt/sumokoin &&\
    rm -r /opt/sumokoin/sumokoin.linux.x* &&\
    apt purge wget -y &&\
    apt autoremove -y


RUN mkdir -p /opt/sumokoin/data


WORKDIR /opt/sumokoin/

EXPOSE 18081 18082
