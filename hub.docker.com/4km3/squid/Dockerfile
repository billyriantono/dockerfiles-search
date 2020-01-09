FROM        alpine:3.4
MAINTAINER  Rodrigo de la Fuente <rodrigo@delafuente.email>

LABEL Description="squid proxy"  \
      Vendor="ACME Products"     \
      Version="1.0"

RUN apk add --no-cache squid

ENTRYPOINT ["/usr/sbin/squid", "-X", "-N"]
