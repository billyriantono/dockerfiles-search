FROM alpine:latest

MAINTAINER Patrick

RUN apk --update add bash vim

ADD https://github.com/hyp530/shadowsocks-go/releases/download/1.1.5/shadowsocks-server-linux64-1.1.5.gz /

ADD config.json /

RUN \
mv shadowsocks-* shadowsocks.gz  && \
gzip -d shadowsocks.gz && \
chmod 755 shadowsocks

#EXPOSE 34501 34502 34503 34504 34505 34506 34507 34508 34509 34510

CMD ["/shadowsocks"]
