FROM yellowblackandwhite/alpine-python3
MAINTAINER Pavel Litvinenko <gerasim13@gmail.com>
USER root

COPY requirements.txt /tmp/
RUN apk --update add build-base python3-dev libffi-dev openssl-dev libxml2-dev libxslt-dev libjpeg-turbo-dev zlib-dev && \
    pip3 install --upgrade -r /tmp/requirements.txt && \
    apk del build-base && \
    rm -rf /root/.cache/pip/* && \
    rm -rf /var/cache/apk/* && \
    rm -rf /tmp/*

USER alpine
