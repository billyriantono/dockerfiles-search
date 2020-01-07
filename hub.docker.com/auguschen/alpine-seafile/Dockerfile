FROM alpine

MAINTAINER Chen Augus <tianhao.chen@gmail.com>

RUN apk update && apk add ca-certificates openssl wget which bash python py-setuptools py-imaging py-mysqldb 

EXPOSE 8000 8082

CMD bash /opt/seafile/startup.sh
