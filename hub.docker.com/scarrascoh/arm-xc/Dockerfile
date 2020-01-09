FROM debian:stretch-slim

LABEL maintainer="scarrascoh.develop@gmail.com" \
      version=1.23.0 \
      description="ARM Cross-Compile Docker image" 

RUN apt update -y && \
    apt install -y git bc build-essential \
      wget gperf bison flex texinfo help2man gawk libncurses-dev file && \
    rm -rf /var/lib/apt/lists/*

ENV WORKDIR /home/arm

RUN groupadd arm && useradd -g arm -d $WORKDIR arm \
    && mkdir $WORKDIR \
    && chown arm:arm $WORKDIR

WORKDIR $WORKDIR

ENV XTOOLNG_VERSION 1.23.0
ENV XTOOLNG_DIR "/opt/x-tools"

# Install Toolchain throught crosstools-NG
RUN wget http://crosstool-ng.org/download/crosstool-ng/crosstool-ng-${XTOOLNG_VERSION}.tar.bz2 && \
    tar -vxf crosstool-ng-${XTOOLNG_VERSION}.tar.bz2 && \
    cd crosstool-ng-${XTOOLNG_VERSION} && \
    ./configure --prefix=${XTOOLNG_DIR} && \
    make && \
    make install && \
    cp ct-ng.comp /etc/bash_completion.d/ && \
    rm -r $WORKDIR/crosstool-ng-${XTOOLNG_VERSION} && \
    rm $WORKDIR/crosstool-ng-1.23.0.tar.bz2 && \
    mkdir $WORKDIR/src

ENV PATH="${PATH}:${XTOOLNG_DIR}/bin"

CMD ["bash"]
