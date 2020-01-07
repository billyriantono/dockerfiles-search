FROM alpine:3.8

RUN apk update && \
    apk add --no-cache python3 && \
    pip3 install --upgrade --no-cache-dir pip setuptools && \
    ln -s /usr/bin/python3 /usr/bin/python
