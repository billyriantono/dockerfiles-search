FROM alpine:latest

ENV FRP_VERSION 0.27.0

RUN wget --no-check-certificate https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_arm.tar.gz && \ 
    tar xzf frp_${FRP_VERSION}_linux_arm.tar.gz && \
    cd frp_${FRP_VERSION}_linux_arm && \
    mkdir /frps && \
    mkdir /frpc && \
    mkdir /frpc/config && \
    mv frps /frps && \
    mv frpc /frpc && \
    cd .. && \
    rm -rf *.tar.gz && \
    rm -rf frp_${FRP_VERSION}_linux_arm

WORKDIR /
EXPOSE 80 443 6000 7000 7500

ENTRYPOINT ["/frpc/frpc", "-c", "/frpc/config/frpc.ini"]
