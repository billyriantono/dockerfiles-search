FROM ubuntu:20.04

MAINTAINER wes <wes.pxw@gmail.com>

RUN apt-get update && \
#   apt-get install -y --no-install-recommends apt-utils && \
    apt-get upgrade -y && \
#   apt-get install -y -m python3-pip python-m2crypto && \
    apt-get install -y shadowsocks-libev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# RUN pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip

ENV SS_SERVER_ADDR 0.0.0.0
ENV SS_SERVER_PORT 54321
ENV SS_PASSWORD Passw0rd!
ENV SS_METHOD aes-256-cfb
ENV SS_TIMEOUT 300

ADD start.sh /start.sh
RUN chmod 755 /start.sh

EXPOSE $SS_SERVER_PORT

CMD ["sh", "-c", "/start.sh"]
