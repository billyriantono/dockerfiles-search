FROM alpine:3.6

RUN apk add --update \
    --no-cache ca-certificates \
    gcc \
    make \
    libffi-dev \
    musl-dev \
    openssl-dev \
    python python-dev \
    py-pip \
  && pip install ansible \
  && rm -rf /var/cache/apk/*
