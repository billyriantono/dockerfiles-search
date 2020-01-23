FROM golang:1.9.2-alpine3.6
RUN apk --update add findutils build-base curl autoconf automake libtool wget git && \
    cd / && \
    git clone https://github.com/openvenues/libpostal && \
    cd /libpostal && \
    ./bootstrap.sh && \
    mkdir /lp && \
    mkdir /lp/data && \
    ./configure --datadir=/lp/data && \
    make && \
    make install && \
    go get github.com/openvenues/gopostal/expand && \
    go get github.com/openvenues/gopostal/parser
WORKDIR $GOPATH