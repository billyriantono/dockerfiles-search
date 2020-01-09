FROM python:3.5.3-alpine

LABEL maintainer=https://github.com/PengBAI

RUN apk add --update curl \
    && curl -O https://bootstrap.pypa.io/get-pip.py \
    && python get-pip.py --user \
    && pip install awscli --upgrade --user \
    && rm -rf /var/cache/apk/* 

RUN sed -i '/^export PATH=/s/$/\:\/root\/\.local\/bin/' /etc/profile

ENV PATH $PATH:/root/.local/bin

CMD aws --version