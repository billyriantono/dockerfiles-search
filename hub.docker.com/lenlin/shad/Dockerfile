FROM debian:jessie
MAINTAINER gal "keepob@163.com"

ADD run.sh /run.sh

RUN apt-get update && \
    apt-get install -y python-pip && \
    pip install shadowsocks && \
    rm -rf /var/lib/apt/lists/* && \
    chmod 755 /run.sh && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
    
ENV PORT=443
ENV KEY=gy.tk
ENV MAC=aes-256-cfb

VOLUME ["/root/data"]
EXPOSE 443
CMD ["/run.sh"]
