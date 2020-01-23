FROM golang:latest as builder

COPY pkgs-install.sh /root/docker/
RUN bash -ex /root/docker/pkgs-install.sh

FROM busybox:glibc
LABEL maintainer="doge.py <doge.py@gmail.com>"

COPY docker-entrypoint.sh /root/docker/

# ca
COPY --from=builder /etc/ssl/certs /etc/ssl/certs

# gost
COPY --from=builder /go/bin/gost /usr/bin/gost

# besttrace
COPY --from=builder /usr/bin/besttrace /usr/bin/besttrace

# tcpping
COPY --from=builder /usr/bin/tcpping /usr/bin/tcpping

# rclone
COPY --from=rclone/rclone:latest /usr/local/bin/rclone /usr/bin/rclone

# v2ray
COPY --from=idoge/v2ray:latest /usr/bin/v2ray /usr/bin/v2ray
COPY --from=idoge/v2ray:latest /etc/v2ray/config.json /etc/v2ray/config.json

ENTRYPOINT ["/bin/sh", "/root/docker/docker-entrypoint.sh"]
CMD ["sh"]