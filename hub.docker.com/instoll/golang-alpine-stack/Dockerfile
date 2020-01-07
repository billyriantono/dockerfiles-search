FROM golang:1.9.2-alpine3.6

RUN echo "Install dependencies" && \
    apk --no-cache add \
      bash \
      build-base \
      git \
      make \
      openssl \
      rsync \
      tidyhtml \
      supervisor && \
    echo "Setup supervisor log directory" && \
    mkdir -p /var/log/supervisor && \
    echo "Install Golang dependency management tool" && \
    go get -u github.com/golang/dep/cmd/dep
