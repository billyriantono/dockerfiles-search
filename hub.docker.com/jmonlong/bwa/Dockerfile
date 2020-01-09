FROM ubuntu:18.04

MAINTAINER jmonlong@ucsc.edu

RUN apt-get update \
        && apt-get install -y --no-install-recommends \
        wget \
        bcftools samtools \
        tabix \
        gcc \
        git \
        time \
        libbz2-dev \
        zlib1g zlib1g-dev \
        make \
        && rm -rf /var/lib/apt/lists/*

WORKDIR /home

RUN wget --no-check-certificate https://github.com/lh3/bwa/releases/download/v0.7.17/bwa-0.7.17.tar.bz2 \
        && tar -xjf bwa-0.7.17.tar.bz2 \
        && cd bwa-0.7.17 \
        && make \
        && cp bwa /bin/ \
        && cd .. \
        && rm -r bwa-0.7.17.tar.bz2 bwa-0.7.17
        
ENTRYPOINT ["bwa"]
