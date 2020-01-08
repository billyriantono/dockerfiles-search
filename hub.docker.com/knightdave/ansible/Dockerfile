FROM python:2.7-alpine

ENV ANSIBLE_VERSION 2.3

RUN apk --update add --virtual deps \
        gcc \
        musl-dev \
        libffi-dev \
        openssl-dev \
        python-dev \
        make \
    && pip install ansible==$ANSIBLE_VERSION \
    && apk del deps \
    && rm -rf /var/cache/apk/*

ENTRYPOINT ["ansible-playbook"]