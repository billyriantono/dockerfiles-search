FROM debian:jessie

LABEL mantainer="André M. Ribeiro dos Santos <andremrsantos@gmail.com>"

RUN apt-get update && \
    apt-get install -yq --no-install-recommends \
        graphviz \
        wget \
        build-essential \
        libopenblas-dev \
        libgsl0-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget --no-check-certificate \
        https://github.com/DReichLab/AdmixTools/archive/v5.0.tar.gz && \
    tar -xvzf v5.0.tar.gz && \
    cd AdmixTools-5.0/src && \
    make clobber && \
    make install && \
    rm -rf v5.0.tar.gz

ENV PATH=$PATH:/AdmixTools-5.0/bin