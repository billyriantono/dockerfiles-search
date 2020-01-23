FROM alpine:latest 
MAINTAINER EasonYang <mail@eason-yang.com>

RUN \   
  apk --update --upgrade add \       
  privoxy \   
  && rm /var/cache/apk/*

ENV FORWARD_SOCKS5_ADDRESS 0.0.0.0
ENV FORWARD_SOCKS5_PORT 8096

EXPOSE 8118

COPY entrypoint.sh /entrypoint.sh
COPY privoxy/conf /conf

ENTRYPOINT ["/entrypoint.sh"]
