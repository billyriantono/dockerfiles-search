FROM alpine:3.9

ENV FRP_VERSION 0.27.0

RUN wget --no-check-certificate https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz && \ 
    tar xzf frp_${FRP_VERSION}_linux_amd64.tar.gz && \
    cd frp_${FRP_VERSION}_linux_amd64 && \
    mkdir -p /etc/frp/ &&  \
    mv frps /frps && \
	mv frpc /frpc && \
    mv frps.ini /frps.ini && \
	mv frpc.ini /frpc.ini && \
    cd .. && \
    rm -rf *.tar.gz && \
    rm -rf frp_${FRP_VERSION}_linux_amd64

WORKDIR /
EXPOSE 7000

ENTRYPOINT ["/frps","-c","/frps.ini"]