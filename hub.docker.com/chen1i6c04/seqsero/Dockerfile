
FROM ubuntu:16.04

MAINTAINER chen1i6c04 <chen1i6c04@gmail.com>

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
    build-essential \
    git \
    make \
    blast2 \
    wget \
    python2.7 \
    python-pip \
    bwa \
    samtools \
    curl && \
    git clone https://github.com/denglab/SeqSero.git && \
    rm -rf /var/cache/apt/* /var/lib/apt/lists/*;


RUN pip install -U biopython


