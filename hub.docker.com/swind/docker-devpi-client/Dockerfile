FROM alpine:3.5

# Install python3 with lxml
RUN apk add --no-cache python3 && \
    apk add --no-cache git && \
    python3 -m ensurepip && \
    apk add --no-cache py3-lxml && \
    apk add --no-cache py3-paramiko && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    pip3 install --no-cache-dir devpi-client && \
    rm -r /root/.cache

RUN ln -s /usr/bin/python3 /usr/bin/python

ONBUILD RUN mkdir -p /code
ONBUILD WORKDIR /code
