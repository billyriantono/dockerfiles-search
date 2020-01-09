FROM        alpine:3.4

MAINTAINER  Rodrigo de la Fuente <rodrigo@delafuente.email>

LABEL Description="OpenVPN"  \
      Vendor="ACME Products" \
      Version="1.0"

RUN apk --no-cache add openvpn
ENTRYPOINT ["/usr/sbin/openvpn"]
