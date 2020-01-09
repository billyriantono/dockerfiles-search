FROM alpine

RUN apk add --no-cache --virtual .build-dependencies unzip wget \
        && apk add --no-cache ca-certificates \
        && cd /tmp \
        && wget http://downloads.rclone.org/rclone-current-linux-amd64.zip \
        && unzip rclone-current-linux-amd64.zip \
        && cp ./rclone-v*-linux-amd64/rclone /usr/sbin \
        && chown root:root /usr/sbin/rclone \
        && chmod 755 /usr/sbin/rclone \
        && apk del .build-dependencies \
        && rm -rf /tmp/*

CMD ["/bin/sh"]
