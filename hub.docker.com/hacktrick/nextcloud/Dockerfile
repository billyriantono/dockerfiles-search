# hacktrick/nextcloud:11-xenial

FROM ubuntu:xenial

ENV NC_VERSION=11.0.3 \
    NC_DOWNLOAD=/tmp \
    NC_BASE=/var/www \
    NC_DATA=/data/nextcloud
ENV NC_HOME=${NC_BASE}/nextcloud

RUN echo "updating system..." \
    && apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        apache2 \
        cron \
        libapache2-mod-php7.0 \
        netcat-openbsd \
        php-apcu \
        php-imagick \
        php-redis \
        php7.0-curl \
        php7.0-gd \
        php7.0-intl \
        php7.0-json \
        php7.0-mbstring \
        php7.0-mcrypt \
        php7.0-mysql \
        php7.0-pgsql \
        php7.0-xml \
        php7.0-zip \
        unzip \
        vim \
        supervisor \
        wget \
    && rm -rf /var/lib/apt/lists/*

RUN echo "downloading nextcloud..." \
    && wget -qP ${NC_DOWNLOAD} https://download.nextcloud.com/server/releases/nextcloud-${NC_VERSION}.zip \
    && wget -qP ${NC_DOWNLOAD} https://download.nextcloud.com/server/releases/nextcloud-${NC_VERSION}.zip.sha256 \
    && cd ${NC_DOWNLOAD} \
    && sha256sum  -c ${NC_DOWNLOAD}/nextcloud-${NC_VERSION}.zip.sha256 \
    && unzip -q nextcloud-${NC_VERSION}.zip -d ${NC_BASE} \
    && mkdir -p ${NC_DATA} \
    && rm -rf ${NC_DOWNLOAD}/nextcloud*

COPY resource/entrypoint.sh resource/docker-wait /usr/local/bin/
COPY resource/nextcloud.a2site /etc/apache2/sites-available/nextcloud.conf
COPY resource/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN echo "configuring apache..." \
    && a2enmod rewrite \
    && a2enmod headers \
    && a2enmod env \
    && a2enmod dir \
    && a2enmod mime \
    && a2dissite 000-default \
    && a2ensite nextcloud

VOLUME ["${NC_DATA}", "${NC_HOME}/config"]

RUN echo "setting file permissions..." \
    && chown -R www-data:www-data \
       ${NC_HOME}/ \
       ${NC_DATA}/ \
    && chmod +x /usr/local/bin/entrypoint.sh /usr/local/bin/docker-wait

ENTRYPOINT ["entrypoint.sh"]

CMD ["/usr/bin/supervisord"]

