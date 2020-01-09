FROM golang:alpine  as builder

WORKDIR /root/docker/

RUN apk upgrade --update \
    && apk add ca-certificates bash curl git make

COPY pkgs-install.sh /root/docker/
RUN bash -ex /root/docker/pkgs-install.sh

FROM scratch

LABEL version="1.0" \
    description="Coredns" \
    by="doge.py" \
    maintainer="doge.py@gmail.com"

# ca
COPY docker.local /docker.local
COPY --from=builder /etc/ssl/certs /etc/ssl/certs
COPY --from=builder /Corefile /Corefile
COPY --from=builder /coredns /coredns

EXPOSE 53 53/udp
ENTRYPOINT ["/coredns"]
