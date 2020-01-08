FROM golang:1.10-alpine

# Install ghr
ENV GHR_VERSION v0.10.2

RUN apk add curl && \
    cd /tmp && \
    curl -L https://github.com/tcnksm/ghr/releases/download/${GHR_VERSION}/ghr_${GHR_VERSION}_linux_amd64.tar.gz -o ghr.tar.gz && \
    tar xfz ghr.tar.gz --strip-components=1 && \
    mv ghr /usr/local/bin/ghr && \
    rm -rf ./*
