FROM rxvc/jdk:8-jdk-alpine

MAINTAINER Rodrigo Vallejo  <rxvallejocj@gmail.com>

RUN apk add --no-cache python3 bash git curl \
    && python3 -m ensurepip \
    && rm -r /usr/lib/python*/ensurepip \
    && pip3 install --upgrade pip setuptools \
    && if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi \
    && if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi \
    && pip install setuptools-git pipreqs \
    && pip install --no-cache-dir git+https://github.com/rxvc/docker_utils.git \
    && rm -r /root/.cache
