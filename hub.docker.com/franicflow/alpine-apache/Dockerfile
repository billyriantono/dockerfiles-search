FROM alpine:3.10
LABEL version="0.6.0" \
      description="Apache2 + PHP 7.3 on Alpine" \
      maintainer="nhuhoai.vo@franicflow.ch"
EXPOSE 80/tcp
COPY ./script/phpinfo.php /var/www/localhost/htdocs/phpinfo.php
COPY ./script/check.php /var/www/localhost/htdocs/check.php
WORKDIR /var/www/localhost/htdocs
RUN apk update && \
    apk add apache2 && \
    apk search -qe php7* | xargs apk add
ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["-X", "-d", "FOREGROUND", "-f", "/etc/apache2/httpd.conf"]
