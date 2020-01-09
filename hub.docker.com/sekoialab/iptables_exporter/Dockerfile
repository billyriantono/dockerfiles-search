FROM golang:1.11 as builder 
RUN go get -v github.com/retailnext/iptables_exporter

FROM debian:9-slim

RUN apt update && \
    apt install iptables -y && \
    rm -fr /var/lib/apt/lists/* 

COPY --from=builder /go/bin/iptables_exporter /usr/local/bin/iptables_exporter
# add capabilities when running this container: 
# CAP_DAC_READ_SEARCH CAP_NET_ADMIN CAP_NET_RAW
# To have access to host iptables, add --net=host option. 

EXPOSE 9455
CMD ["iptables_exporter"]
