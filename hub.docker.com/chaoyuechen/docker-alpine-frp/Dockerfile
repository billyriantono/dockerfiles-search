FROM alpine:3.6

ENV FRP_VERSION=0.30.0
ENV FRP_DOWNLOAD_URL=https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz

ADD ${FRP_DOWNLOAD_URL} .
ADD server/frps.ini /etc/

RUN tar -zxvf frp_${FRP_VERSION}_linux_amd64.tar.gz \
    && mv frp_${FRP_VERSION}_linux_amd64/frps /usr/local/bin \
    && rm -rf frp_${FRP_VERSION}_linux_amd64 frp_${FRP_VERSION}_linux_amd64.tar.gz
 
EXPOSE 7000 7500
CMD ["frps","-c","/etc/frps.ini"]