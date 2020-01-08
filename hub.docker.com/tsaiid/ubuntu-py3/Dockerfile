FROM ubuntu:16.04
MAINTAINER I-Ta Tsai <itsai@gmail.com>

RUN apt-get update && apt-get upgrade -y --no-install-recommends && \
	apt-get install -y --no-install-recommends \
        tzdata \
        python3-minimal python3-pip python3-setuptools python3-dev && \
    apt-get -y autoremove && apt-get clean && \
    rm -rf /usr/share/doc && rm -rf /usr/share/man && \
    rm -rf /var/lib/apt/lists/*

