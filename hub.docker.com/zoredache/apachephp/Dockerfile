FROM debian:buster-slim

RUN export TERM="xterm"; \
    export DATE_TIMEZONE="Etc/UTC" ; \
    apt-get update ; \
    </dev/null DEBIAN_FRONTEND=noninteractive \
    apt-get install tini; \
    apt-get -yq install \
	apache2 \
	libapache2-mod-php \
        cronolog \
	php \
	php-bz2 \
	php-cli \
	php-common \
	php-curl \
	php-dev \
	php-enchant \
	php-gd \
	php-gmp \
	php-intl \
	php-json \
        php-mbstring \
	php-mysql \
	php-opcache \
	php-phpdbg \
	php-pspell \
	php-readline \
	php-recode \
	php-tidy \
	php-xsl \
	php-zip ; \
    a2enmod rewrite actions include

EXPOSE 80

CMD ["tini", "--", "/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
