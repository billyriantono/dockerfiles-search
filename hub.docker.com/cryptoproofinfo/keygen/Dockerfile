FROM alpine:3.4
MAINTAINER Derren Desouza <derrend@yahoo.co.uk>

RUN apk add --no-cache git py-setuptools && \
    cd && \
    git clone https://github.com/cryptoproofinfo/pycoin.git && \
    cd pycoin && \
    python setup.py install && \
    cd && \
    rm -rf pycoin && \
    apk del git
