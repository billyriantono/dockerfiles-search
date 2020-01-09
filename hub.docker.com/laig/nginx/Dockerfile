FROM nginx:alpine
MAINTAINER Giampiero Lai <giampiero.lai@gmail.com>

RUN apk update \ 
    && apk add --no-cache openssh-client unzip curl bison git openssl \
    && apk upgrade

RUN mkdir -p /etc/certs/
RUN openssl req -new -x509 -nodes -out /etc/certs/server.pem -keyout /etc/certs/server.key -days 3650 -subj '/CN=localhost'