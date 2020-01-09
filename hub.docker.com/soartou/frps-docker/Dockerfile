FROM alpine:latest
RUN apk update && apk add tzdata wget
RUN cp -r -f /usr/share/zoneinfo/Hongkong /etc/localtime
#ADD frps /usr/local/bin/
RUN mkdir /download && cd /download \
    && wget -N --no-check-certificate https://github.com/fatedier/frp/releases/download/v0.21.0/frp_0.21.0_linux_amd64.tar.gz \
    && tar xzf frp_0.21.0_linux_amd64.tar.gz
RUN find /download -name "frps" -exec cp {}  /usr/local/bin/frps \;
RUN rm -rf /download
run apk del tzdata wget
RUN chmod +x /usr/local/bin/frps
CMD ["frps", "-c", "/etc/frp/frps.ini"]
