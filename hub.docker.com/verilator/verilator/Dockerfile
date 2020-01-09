FROM ubuntu:18.04

RUN apt-get update && apt-get install -y git build-essential  autoconf flex bison \
                                         bc perl python3

ARG REPO=https://github.com/wallento/verilator
ARG SOURCE_COMMIT=master


WORKDIR /tmp

RUN git clone ${REPO} verilator && \
    cd verilator &&\
    git checkout ${SOURCE_COMMIT} && \
    autoconf && \
    ./configure && \
    make -j `nproc` && \
    make install && \
    cd .. && \
    rm -r verilator

ADD verilator-wrap.sh /usr/local/bin/verilator-wrap.sh

WORKDIR /work

ENTRYPOINT [ "/usr/local/bin/verilator-wrap.sh" ]
