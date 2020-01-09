FROM alpine:3.5

MAINTAINER yikyo <yikyo666@gmail.com>

RUN apk add --update --no-cache py-pip 

RUN pip install shadowsocks

ENV SERVER_ADDR 0.0.0.0
ENV SERVER_PORT 8388
ENV LOCAL_ADDR 0.0.0.0
ENV LOCAL_PORT 1080
ENV PASSWORD password
ENV METHOD aes-256-cfb
ENV TIMEOUT 300

EXPOSE $SERVER_PORT

ENTRYPOINT /usr/bin/sslocal -s $SERVER_ADDR -p $SERVER_PORT -b $LOCAL_ADDR -l $LOCAL_PORT -k $PASSWORD -m $METHOD -t $TIMEOUT 
