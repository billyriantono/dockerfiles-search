FROM alpine:3.1

MAINTAINER Wharsojo

RUN apk add --update nginx  &&\
    mkdir  /tmp/nginx       &&\
    rm -rf /var/cache/apk/*

EXPOSE 80 

CMD ["nginx", "-g", "daemon off;"]