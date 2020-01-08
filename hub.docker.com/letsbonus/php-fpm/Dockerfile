FROM letsbonus/php-cli:5.6-dev

RUN apk add --no-cache \
    apache-ant \
    cloc \
    php5-fpm \
    supervisor \
    unzip \
    fcgi \
 && sed -i 's@listen = 127.0.0.1:9000@listen = [::]:9000@' /etc/php5/php-fpm.conf \
 && sed -i 's@user = nobody@user = root@' /etc/php5/php-fpm.conf \
 && sed -i 's@group = nobody@group = root@' /etc/php5/php-fpm.conf \
 && sed -i 's@;pm.status_path = /status@pm.status_path = /fpm-status@' /etc/php5/php-fpm.conf \
 && sed -i 's@;ping.path = /ping@ping.path = /fpm-ping@' /etc/php5/php-fpm.conf

COPY dev/supervisord.conf.fpm-56 /etc/supervisor/conf.d/supervisord.conf

EXPOSE 9000

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
