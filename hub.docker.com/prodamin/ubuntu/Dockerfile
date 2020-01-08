FROM ubuntu:18.04

RUN apt-get update \ 
    && apt-get install -y curl less vim wget tcpdump git \
    && apt-get install -y screen apt-transport-https iputils-ping \
    && apt-get install -y telnet apache2 \
    ca-certificates tree dnsutils \
    software-properties-common \
    python-pip && pip install --upgrade pip \ 
    && apt-get install -y python3-pip && pip3 install --upgrade pip

