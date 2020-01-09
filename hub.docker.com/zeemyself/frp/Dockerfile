FROM alpine:latest

ARG VERSION=0.24.1
ARG FRP_URL=https://github.com/fatedier/frp/releases/download/v${VERSION}/frp_${VERSION}_linux_amd64.tar.gz

RUN mkdir -p /frp \
    && cd /frp\
    && wget -qO- ${FRP_URL} | tar xz \
    && mv frp_*/frpc /usr/local/bin \
    && mv frp_*/frps /usr/local/bin

VOLUME /frp

ENV ARGS=frps

CMD ${ARGS} -c /frp/${ARGS}.ini
