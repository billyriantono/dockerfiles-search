# version: 0.0.2
FROM ubuntu:16.04
MAINTAINER reqsun
RUN apt-get update
RUN apt-get install -y python-pip
RUN pip install shadowsocks
RUN ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start
EXPOSE 443