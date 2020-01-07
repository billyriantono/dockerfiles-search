FROM amartha/go-alpine-cloudsdk-builder:latest

RUN echo "INSTALL GLIDE"
ENV GLIDE_VERSION 0.13.3

ENV GLIDE_DOWNLOAD_URL https://github.com/Masterminds/glide/releases/download/v${GLIDE_VERSION}/glide-v${GLIDE_VERSION}-linux-amd64.tar.gz

RUN apk add --update ca-certificates \
    && apk add curl git coreutils \
    && rm /var/cache/apk/*

RUN curl -fsSL "$GLIDE_DOWNLOAD_URL" -o glide.tar.gz \
    && tar -xzf glide.tar.gz \
    && mv linux-amd64/glide /usr/bin/ \
    && rm -r linux-amd64 \
    && rm glide.tar.gz
    
RUN echo "INSTALL CODECOV"
RUN apk add mercurial
RUN curl -sSL https://codecov.io/bash | bash

# Install coverage tools to produce coverage reports
RUN go get github.com/wadey/gocovmerge && \
	go get github.com/axw/gocov/gocov && \
	go get github.com/AlekSi/gocov-xml
    
