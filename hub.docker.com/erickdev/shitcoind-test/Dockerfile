FROM ubuntu:16.04

MAINTAINER Erick DEV TEAM <erickdevartworks@outlook.com>
LABEL maintainer="Erick DEV TEAM <erickdevartworks@outlook.com>"

ENV S6_FIX_ATTRS_HIDDEN=1
ENV SRC_DIR /usr/local/src/shitcoin
RUN echo "fs.file-max = 65535" > /etc/sysctl.conf

RUN apt-get update -y && apt-get install -y    git \
                       build-essential \
                       libtool \
                       autotools-dev \
                       automake \
                       pkg-config \
                       libssl-dev \
                       libevent-dev \
                       bsdmainutils \
                       libboost-system-dev \
                       libboost-filesystem-dev \
                       libboost-chrono-dev \
                       libboost-program-options-dev \
                       libboost-test-dev \
                       libboost-thread-dev \
                       software-properties-common \
                       libminiupnpc-dev \
                       libzmq3-dev \
                       libqt4-dev libprotobuf-dev protobuf-compiler\
                       python3 \
                       libboost-thread-dev libboost-dev libevent-1.4-2 \
                       libqrencode-dev libminiupnpc-dev git \
                       g++ \
                       make \
                       automake       
RUN apt-get update && apt-get install software-properties-common -y \
                      && add-apt-repository ppa:bitcoin/bitcoin \
		      && apt-get update -y \
		      && apt-get install libdb4.8-dev libdb4.8++-dev -y \
	              && git clone https://github.com/erickdevartworks/core-test-1.0.0.git \
                      && tar -zxvf core-test-1.0.0/core-test-1.0.0.tar.gz \
		      && strip core-test-1.0.0/shitcoind core-test-1.0.0/shitcoin-cli core-test-1.0.0/shitcoin-tx \
	              && cp core-test-1.0.0/shitcoind /usr/local/bin/ \
		      && cp core-test-1.0.0/shitcoin-cli /usr/local/bin/ \
	              && cp core-test-1.0.0/shitcoin-tx /usr/local/bin/

VOLUME /root/.Shitcoin

EXPOSE 4280

EXPOSE 4281

EXPOSE 4282

WORKDIR /root

COPY rootfs /
ADD env/.bashrc /root/
RUN apt-get -y install curl && curl -L -s https://github.com/just-containers/s6-overlay/releases/download/v1.21.2.1/s6-overlay-amd64.tar.gz \
    | tar xzf - -C /

ENTRYPOINT [ "/init" ]
