FROM busybox:latest
MAINTAINER David Lee Crites <lee@critesclan.com>

RUN mkdir -pm 0777 /var/lib/mysql && \
    mkdir -pm 0777 /var/www/html && \
    echo '#!/bin/sh' 1>/entrypoint.sh && \
    echo 'tail -f /dev/null' 1>>/entrypoint.sh && \
    chmod 755 /entrypoint.sh

VOLUME [ "/var/lib/mysql", "/var/www/html" ]
ENTRYPOINT ["/entrypoint.sh"]
CMD ["busybox"]
