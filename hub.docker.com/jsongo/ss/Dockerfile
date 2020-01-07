FROM python:2.7-alpine3.7

LABEL author="jsongo<jsongo@qq.com>"

RUN pip install --upgrade pip
RUN pip install shadowsocks
COPY ./run.sh /

EXPOSE 443

ENTRYPOINT /bin/sh -c /run.sh
