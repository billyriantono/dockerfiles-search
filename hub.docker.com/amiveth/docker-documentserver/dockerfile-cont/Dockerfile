FROM alpine:latest

RUN apk add --update curl
# Get latest release version and download it
RUN export PG_VERSION=$(curl -Is https://github.com/prometheus/pushgateway/releases/latest | grep Location | cut -d '/' -f8 | cut -c2-6) && \
    cd /tmp && \ 
    wget https://github.com/prometheus/pushgateway/releases/download/v${PG_VERSION}/pushgateway-${PG_VERSION}.linux-armv7.tar.gz && \
    tar xzvf pushgateway-${PG_VERSION}.linux-armv7.tar.gz && \
    mv pushgateway-${PG_VERSION}.linux-armv7/pushgateway /pushgateway && \
    rm -rf pushgateway-${PG_VERSION}.linux-armv7* && \
    apk del curl

CMD ["/pushgateway"]
