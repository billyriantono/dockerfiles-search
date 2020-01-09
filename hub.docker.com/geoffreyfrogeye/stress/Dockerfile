FROM alpine:3.6

ENV version 1.0.4

RUN apk add --update make gcc musl-dev && \
    wget http://people.seas.harvard.edu/~apw/stress/stress-$version.tar.gz && \
    tar xf stress-$version.tar.gz && \
    cd stress-$version && \
    ./configure && \
    make install && \
    cd .. && \
    rm -rf stress-$version.tar.gz stress-$version && \
    apk del make gcc musl-dev
