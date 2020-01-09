FROM alpine:edge

RUN apk update && apk add tzdata wget
RUN cp -r -f /usr/share/zoneinfo/Hongkong /etc/localtime
#ADD frpc /usr/local/bin/
RUN mkdir /download && cd /download \
    && wget -N --no-check-certificate https://github.com/fatedier/frp/releases/download/v0.21.0/frp_0.21.0_linux_amd64.tar.gz \
    && tar xzf frp_0.21.0_linux_amd64.tar.gz
RUN find /download -name "frpc" -exec cp {}  /usr/local/bin/frpc \;
RUN chmod +x /usr/local/bin/frpc
ADD frpc.ini /etc/frp/

CMD ["frpc", "-c", "/etc/frp/frpc.ini"]
