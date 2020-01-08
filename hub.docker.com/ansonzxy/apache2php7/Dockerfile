FROM alpine:latest
LABEL maintainer="Russ Mckendrick <russ@mckendrick.io>"
LABEL description="This example Dockerfile installs Apache & PHP"

ENV PHPVERSION 7

RUN echo "151.101.188.249  dl-cdn.alpinelinux.org" >> /etc/hosts && \
    apk add --update apache2 php${PHPVERSION}-apache2 php${PHPVERSION} && \
    rm -rf /var/cache/apk* && \
    mkdir -p /run/apache2/ && \
    rm -rf /var/www/localhost/htdocs/index.html && \
    echo "<?php phpinfo(); ?>" > /var/www/localhost/htdocs/index.php && \
    chmod 755 /var/www/localhost/htdocs/index.php

EXPOSE 80/tcp

ENTRYPOINT ["httpd"]
CMD ["-D", "FOREGROUND"]
