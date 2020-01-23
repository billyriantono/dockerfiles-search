FROM ubuntu:18.10
RUN cd ~;\
    apt-get update ;\
    apt-get upgrade -y;\
    apt-get install  shadowsocks-libev simple-obfs -y;\
    apt-get clean;\
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
ENV SERVER_PORT=51200
ENV PASSWORD=0ooOOO@
ENV METHOD=aes-256-gcm
ENV TIMEOUT=300
ENV DNS_ADDR=8.8.8.8
ENV OPTIONS="--plugin obfs-server --plugin-opts obfs=http;fast-open;failover=bing.com"
ENV BIND_IP=0.0.0.0
EXPOSE 51200/tcp
EXPOSE 51200/udp
# CMD ["/bin/sh","-c","/usr/bin/ss-server -s $BIND_IP -p $SERVER_PORT -k $PASSWORD -m $METHOD -t $TIMEOUT -d $DNS_ADDR --fast-open -u $OPTIONS"]
