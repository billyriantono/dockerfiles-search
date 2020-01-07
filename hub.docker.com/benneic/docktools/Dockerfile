FROM alpine:latest

RUN apk update && apk upgrade && \
    apk --update add \
    iputils iproute2 net-tools tcpdump \
    ethtool iperf findutils bash \
    netcat-openbsd nmap \
    git curl apache2-utils nghttp2 \
    && rm -rf /var/cache/apk/*
    
CMD ["bash"]
