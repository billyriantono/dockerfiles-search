FROM ubuntu:bionic

RUN apt-get update && \
    apt-get install -y openconnect python3 python3-pip git ocproxy && \
    apt-get clean && \
    rm -rf /var/cache/apt/* && \
    rm -rf /var/lib/apt/lists/* && \
    pip3 install ansible==2.5.2

