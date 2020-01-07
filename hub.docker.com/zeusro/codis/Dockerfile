FROM golang:1.12
LABEL maintainer="https://github.com/zeusro"
ENV GOPATH /gopath
ENV CODIS  ${GOPATH}/src/github.com/CodisLabs/codis
ENV PATH   ${GOPATH}/bin:${PATH}:${CODIS}/bin
COPY . ${CODIS}

RUN apt-get update  \
    && apt-get install -y autoconf \
    && make -C ${CODIS} distclean \
    && make -C ${CODIS} build-all

WORKDIR /codis
