FROM golang:1.10-alpine3.7

RUN apk add --update build-base cmake libstdc++ git linux-headers

WORKDIR /work
ADD Makefile /work/Makefile
RUN make install
