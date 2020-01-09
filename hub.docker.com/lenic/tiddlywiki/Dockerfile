# MIT License
# Copyright (c) 2017 Lenic <Lenic@live.cn>

FROM node:alpine
LABEL author="Lenic <Lenic@live.cn>"

VOLUME /data
WORKDIR /data

EXPOSE 8080

ENV TW_PORT=8080 \
  TW_ROOTTIDDLER=$:/core/save/all \
  TW_RENDERTYPE=text/plain \
  TW_SERVETYPE=text/html \
  TW_USERNAME="" \
  TW_PASSWORD="" \
  TW_HOST=0.0.0.0 \
  TW_PATHPREFIX=""

RUN npm i -g tiddlywiki

ADD init-and-run /usr/local/bin/init-and-run

CMD ["/bin/sh","/usr/local/bin/init-and-run"]
