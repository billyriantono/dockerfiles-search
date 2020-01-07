FROM alpine:3.8

LABEL maintainer "Levent SAGIROGLU <LSagiroglu@gmail.com>"

RUN apk add --update --no-cache tini s6 ca-certificates tzdata && \	
    update-ca-certificates && \
    cp /usr/share/zoneinfo/Europe/Istanbul /etc/localtime && \
    echo "Europe/Istanbul" >  /etc/timezone && \
    apk del tzdata
