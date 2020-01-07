FROM alpine:latest

RUN apk add --update-cache \
    python \
    python-dev \
    py-pip \
    build-base \
    bash \
    curl \
    git \
  && pip install --upgrade pip \
  && pip install virtualenv \
  && rm -rf /var/cache/apk/*


