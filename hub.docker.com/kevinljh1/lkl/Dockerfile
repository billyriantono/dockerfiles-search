FROM debian:latest

MAINTAINER wuqz <wuqinzhong*gmail.com>

RUN apt-get update
RUN apt-get install -y curl build-essential
RUN apt-get install -y nodejs
RUN apt-get install -y wget
RUN apt-get install -y unzip
RUN apt-get install -y python
RUN apt-get install -y libsodium-dev
RUN apt-get install -y libcap-dev
RUN apt-get install -y unzip
RUN apt-get install -y iftop

EXPOSE 17519/udp
EXPOSE 17518/udp
EXPOSE 17520/tcp
EXPOSE 17517/tcp

RUN wget https://github.com/keviljh3/docker_java_fs_kcp_ssr/raw/master/html.js
RUN wget --no-check-certificate https://github.com/shadowsocksrr/shadowsocksr/archive/akkariiin/dev.zip -O /dev.zip
RUN unzip dev.zip

COPY  *.* /root/lkl/

RUN apt-get update ;\
    apt-get install -y iptables haproxy ;\
    chmod a+x /root/lkl/start.sh 

CMD  /root/lkl/start.sh
