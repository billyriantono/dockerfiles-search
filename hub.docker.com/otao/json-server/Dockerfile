FROM node:alpine

MAINTAINER JTao <954463838@qq.com>  

RUN npm install -g json-server

VOLUME ["/var/db"]

WORKDIR "/var/db"

EXPOSE 3000

ENTRYPOINT ["json-server"]