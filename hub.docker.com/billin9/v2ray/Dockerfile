FROM alpine:3.5
RUN apk add --no-cache --virtual .build-deps ca-certificates curl bash && \
    curl https://install.direct/go.sh | bash && \
    rm -rf /usr/bin/v2ray/geoip.dat /usr/bin/v2ray/geosite.dat && \
    chgrp -R 0 /etc/v2ray && \
    chmod -R g+rwX /etc/v2ray && \
    apk del .build-deps
COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT /entrypoint.sh
