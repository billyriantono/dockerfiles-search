FROM debian:stretch
MAINTAINER Alexander Shevchenko <kudato@me.com>

ENV DEBIAN_VERSION stretch
ENV DEBIAN_FRONTEND noninteractive
ENV TZ Europe/Moscow

ENV HTTP 80
ENV HTTPS false

ENV SSH_PORT ${HTTP}22

ENV FQDN example.com
ENV EMAIL mail@example.com

ENV LETSENCRYPT false

ENV PROCESSES nginx php cron cloudcmd ssh

ENV USERNAME user
ENV PASSWORD pass

ENV UNIXNAME www-data
ENV USER_DIR /srv

ENV SSH_PERMIT_ROOT no
ENV SSH_PERMIT_PASS yes

ENV SSL_KEY /etc/letsencrypt/ssl.key
ENV SSL_CERT /etc/letsencrypt/ssl.crt

ENV PHP_VERSION 7.1

ENV PHP_MEMORY 64M
ENV PHP_PM_MAX 5
ENV PHP_PM_START 1
ENV PHP_PM_SPARE_MIN 1
ENV PHP_PM_SPARE_MAX 2

ENV PHP_VERSIONS_SUPPORT 5.6 7.0 7.1
ENV PHP_DISPLAY_ERROR On
ENV PHP_SHORT_OPEN_TAG On
ENV PHP_CONFIG_ENCODING UTF-8
ENV PHP_CONFIG_FUNCOVER 2
ENV PHP_UPLOAD_MAX_SIZE 1024M
ENV PHP_POST_MAX_SIZE 1024M

ENV TEMPLATES_CONFIG /templates_conf
ADD /conf ${TEMPLATES_CONFIG}
ADD /*.sh /
RUN chmod +x /*.sh && \
	ln -sf /healthcheck.sh /usr/bin/healthcheck && \
	ln -sf /magic.sh /usr/bin/magic && \
	magic setup_base
RUN magic setup_nginx
RUN magic setup_php

HEALTHCHECK --retries=3 --interval=15s --timeout=5s CMD healthcheck
ENTRYPOINT ["magic"]
CMD ["run"]




