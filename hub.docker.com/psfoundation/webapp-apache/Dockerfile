FROM debian:stretch-slim

LABEL maintainers="Przemek Szalko <przemek@rentcars.pl>"
ARG DEBIAN_FRONTEND=noninteractive

RUN apt update \
    && apt install -y --no-install-recommends \
    ca-certificates \
    apt-transport-https \
    curl \
    cron \
    apache2 \
    && rm -rf /etc/apache2/sites-enabled/* \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/ \
    && ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime \
    && echo "Europe/Warsaw" > /etc/timezone
    
RUN curl -so /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg \
    && sh -c 'echo "deb https://packages.sury.org/php/ stretch main" > /etc/apt/sources.list.d/php.list' \
    && apt-get update \
    && apt install -y --no-install-recommends \
    php7.2 libapache2-mod-php7.2 \
    php7.2-gd php7.2-mysql php7.2-curl php7.2-xml \
    php7.2-mbstring php7.2-opcache php7.2-json \
    php-redis \
    php-xdebug \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/    

COPY conf/php-7.2/*.ini /etc/php/7.2/mods-available/
COPY bin/php-xdebug.sh /usr/bin/php-xdebug
COPY conf/apache2/* /etc/apache2/conf-enabled/
COPY bin/apache2-foreground.sh /usr/local/bin

# Apache + PHP requires preforking Apache for best results
RUN a2dismod mpm_event \
    && a2enmod mpm_prefork \
    # enable other required modules
    && a2enmod rewrite headers expires proxy proxy_http
        
# Apache logs should go to stdout / stderr
RUN set -ex \
	&& . "/etc/apache2/envvars" \
	&& ln -sfT /dev/stderr "$APACHE_LOG_DIR/error.log" \
	&& ln -sfT /dev/stdout "$APACHE_LOG_DIR/access.log" \
	&& ln -sfT /dev/stdout "$APACHE_LOG_DIR/other_vhosts_access.log" \
    # Remove LogFormat vhost_combined - will be added later in conf/apache2/logs.conf
    && sed -i 's/LogFormat.*vhost_combined//' /etc/apache2/apache2.conf


EXPOSE 80

CMD ["apache2-foreground.sh"]
