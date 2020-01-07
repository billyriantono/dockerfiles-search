FROM busybox

ADD https://github.com/shadowsocks/shadowsocks-go/releases/download/1.2.1/shadowsocks-server.tar.gz /tmp/shadowsocks-server.tar.gz

RUN cd /tmp \
  && tar -xzvf shadowsocks-server.tar.gz \
  && cp shadowsocks-server /usr/bin \
  && rm -rf /tmp/shadowsocks-server*

ENV SS_SERVER 0.0.0.0
ENV SS_SERVER_PORT 10086
ENV SS_PASSWORD password
ENV SS_METHOD aes-256-cfb
ENV SS_TIMEOUT 300

EXPOSE $SS_SERVER_PORT

ENTRYPOINT shadowsocks-server -s $SS_SERVER -p $SS_SERVER_PORT -k $SS_PASSWORD -m $SS_METHOD -t $SS_TIMEOUT
