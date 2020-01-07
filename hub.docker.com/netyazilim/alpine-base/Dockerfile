FROM alpine:3.10

LABEL maintainer "Levent SAGIROGLU <LSagiroglu@gmail.com>"

RUN apk add --upgrade --no-cache tini s6 ca-certificates tzdata && \	
    update-ca-certificates && \
    cp /usr/share/zoneinfo/Europe/Istanbul /etc/localtime && \
    echo "Europe/Istanbul" >  /etc/timezone && \
    apk del tzdata
