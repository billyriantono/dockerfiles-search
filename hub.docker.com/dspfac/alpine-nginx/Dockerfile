FROM gliderlabs/alpine:latest
MAINTAINER Yue Chen "dspfac@gmail.com"

RUN apk-install nginx && mkdir /tmp/nginx

EXPOSE 80
ENV DISCOVER web-server:80


CMD ["nginx", "-g", "daemon off; error_log stderr info;"]


