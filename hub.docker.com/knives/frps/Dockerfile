FROM ubuntu as builder

ENV FRP_VERSION 0.24.1

RUN apt-get update \
  && apt-get install -y wget
RUN wget -O /tmp/frp.tar.gz https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_amd64.tar.gz
RUN cd /tmp && tar -xzf frp.tar.gz && mv frp_${FRP_VERSION}_linux_amd64 frp_linux_amd64

FROM alpine

WORKDIR /opt/frps

COPY --from=builder /tmp/frp_linux_amd64/frps* /opt/frps/

ENTRYPOINT ["/opt/frps/frps", "-c", "/opt/frps/frps.ini"]
