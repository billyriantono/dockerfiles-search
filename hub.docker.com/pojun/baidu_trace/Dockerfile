FROM alpine:latest
MAINTAINER 383057973@qq.com
ENV NPM_CONFIG_LOGLEVEL info
COPY web-demo-v3/ /app/
WORKDIR /app/web-demo-v3
RUN apk update && apk add nodejs
RUN npm install -g fis3 && npm install
RUN fis3 release deamo
CMD fis3 server start && /bin/sh