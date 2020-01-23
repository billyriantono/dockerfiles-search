FROM ubuntu:latest

RUN apt-get update && apt-get -y upgrade \
    && apt-get install --yes build-essential gcc-multilib apt-utils zlib1g-dev wget \
    && wget "https://github.com/lh3/bwa/archive/0.7.12.tar.gz" \
    && tar xvfz 0.7.12.tar.gz \
    && cp -r /bwa-0.7.12/* /usr/bin	

RUN cd /usr/bin && make \
    && chmod 777 /usr/bin/bwa
