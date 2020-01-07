FROM golang:latest
MAINTAINER Terry Ding

RUN echo "deb http://deb.debian.org/debian stretch-backports main" >> /etc/apt/sources.list && \
    apt-get update && \
    apt-get -y install libz-dev libbz2-dev libsnappy-dev && \
    apt-get -y -t stretch-backports install librocksdb-dev && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /root

CMD ["bash"]
