FROM golang:1.11.0 as nwn-order-builder
RUN apt update \
    && apt upgrade -y \
    && rm -r /var/lib/apt/lists /var/cache/apt \
    && git clone https://github.com/Urothis/nwn-order.git \
    && cd nwn-order \
    && git checkout dev \
    && cd go \
    && go mod download \
    && go build -o ./bin/order \
    && mv bin/order /usr/local/bin/order
FROM ubuntu:latest
LABEL maintainer "urothis@gmail.com"
COPY --from=nwn-order-builder /usr/local/bin/order /nwn-order/order
RUN apt update \
    && apt upgrade -y \
    && apt-get install ca-certificates -y\
    && apt-get clean \
    && rm -r /var/lib/apt/lists /var/cache/apt \
    && mkdir logs \
    && chmod +x ./nwn-order/order \
    && cd nwn-order
ENTRYPOINT [ "order" ]