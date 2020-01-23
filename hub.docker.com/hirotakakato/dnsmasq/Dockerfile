FROM alpine:latest

RUN set -eux; \
    apk add --no-cache dnsmasq; \
    echo -e '#!/bin/sh -eu\necho "${DNSMASQ_CONF:-}" > /etc/dnsmasq.d/dnsmasq.conf\nexec dnsmasq -k -8 /dev/stdout' \
      | install -m 755 /dev/stdin /cmd.sh

CMD ["/cmd.sh"]
