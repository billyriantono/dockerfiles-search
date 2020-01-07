FROM alpine:3.8

RUN apk add --update --no-cache --virtual=build-dependencies build-base curl-dev python3-dev \
    && apk add --update --no-cache bash curl libcurl python3 ca-certificates \
    && python3 -m ensurepip \
    && pip3 install --upgrade pip setuptools \
    && pip3 install pycurl \
    && if [ ! -e /usr/bin/pip ]; then ln -s /usr/bin/pip3 /usr/bin/pip ; fi \
    && if [ ! -e /usr/bin/python ]; then ln -s /usr/bin/python3 /usr/bin/python; fi \
    && apk update \
    && apk del --update build-dependencies \
    && rm -r /usr/lib/python*/ensurepip \
    && rm -r /root/.cache

