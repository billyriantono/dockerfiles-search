FROM golang:latest as builder

RUN set -x \
 && go get github.com/fullstorydev/grpcurl \
 && go install github.com/fullstorydev/grpcurl/cmd/grpcurl

FROM debian:stretch

RUN set -x \
 && apt-get update \
 && apt-get -y install \
    redis-tools \
    mysql-client \
    postgresql-client \
    dnsutils \
    telnet \
    net-tools \
    traceroute \
    mtr \
    tcpdump \
    nmap \
    curl \
    vim \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

COPY --from=builder /go/bin/grpcurl /usr/local/bin/grpcurl

RUN set -x \
 && chmod 755 /usr/local/bin/grpcurl

CMD ["sh", "-c", "tail -f /dev/null"]
