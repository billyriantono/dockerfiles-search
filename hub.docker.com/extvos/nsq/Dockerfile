FROM nsqio/nsq:latest
MAINTAINER  "Mingcai SHEN <archsh@gmail.com>"

RUN apk update && apk add --no-cache tzdata \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" >  /etc/timezone \
    && apk del tzdata \
    && apk add --no-cache curl wget ca-certificates \
    && update-ca-certificates