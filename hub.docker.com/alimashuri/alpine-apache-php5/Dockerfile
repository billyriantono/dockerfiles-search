FROM nimmis/alpine-micro:edge

MAINTAINER Ali Mashuri <ali@mashuri.web.id>

COPY root/. /

# Environments
ENV TIMEZONE            Asia/Jakarta
ENV PHP_MEMORY_LIMIT    512M
ENV MAX_UPLOAD          50M
ENV PHP_MAX_FILE_UPLOAD 200
ENV PHP_MAX_POST        100M

RUN apk update && apk upgrade && \

    # Make info file about this build
    printf "Build of alimashuri/alpine-lamp, date: %s\n"  `date -u +"%Y-%m-%dT%H:%M:%SZ"` >> /etc/BUILD && \

    apk add --update apache2 libxml2-dev apache2-utils && \
    apk add --update tzdata && \
    cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo "${TIMEZONE}" > /etc/timezone && \
    apk add --update \
        php5-mcrypt \
        php5-soap \
        php5-openssl \
        php5-gmp \
        php5-pdo_odbc \
        php5-json \
        php5-dom \
        php5-pdo \
        php5-zip \
        php5-mysql \
        php5-sqlite3 \
        php5-apcu \
        php5-pdo_pgsql \
        php5-bcmath \
        php5-gd \
        php5-xcache \
        php5-odbc \
        php5-pdo_mysql \
        php5-pdo_sqlite \
        php5-gettext \
        php5-xmlreader \
        php5-xmlrpc \
        php5-bz2 \
        php5-memcache \
        php5-mssql \
        php5-iconv \
        php5-pdo_dblib \
        php5-curl \
        php5-ctype \
        php5-phar \
        php5-apache2 \
        php5-cli && \
    mkdir /web/ && chown -R apache.www-data /web && \
   
    # Set environments php5
    sed -i "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" /etc/php5/php.ini && \
    sed -i "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" /etc/php5/php.ini && \
    sed -i "s|;*upload_max_filesize =.*|upload_max_filesize = ${MAX_UPLOAD}|i" /etc/php5/php.ini && \
    sed -i "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" /etc/php5/php.ini && \
    sed -i "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" /etc/php5/php.ini && \
    sed -i "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|i" /etc/php5/php.ini && \
    
    # Set environments apache2
    sed -i 's#^DocumentRoot ".*#DocumentRoot "/web/html"#g' /etc/apache2/httpd.conf && \
    sed -i 's#AllowOverride none#AllowOverride All#' /etc/apache2/httpd.conf && \
    sed -i 's#^ServerRoot .*#ServerRoot /web#g'  /etc/apache2/httpd.conf && \
    sed -i 's/^#ServerName.*/ServerName webproxy/' /etc/apache2/httpd.conf && \
    sed -i 's#^IncludeOptional /etc/apache2/conf#IncludeOptional /web/config/conf#g' /etc/apache2/httpd.conf && \
    sed -i 's#PidFile "/run/.*#Pidfile "/web/run/httpd.pid"#g'  /etc/apache2/conf.d/mpm.conf && \
    sed -i 's#Directory "/var/www/localhost/htdocs.*#Directory "/web/html" >#g' /etc/apache2/httpd.conf && \
    sed -i 's#Directory "/var/www/localhost/cgi-bin.*#Directory "/web/cgi-bin" >#g' /etc/apache2/httpd.conf && \

    sed -i 's#/var/log/apache2/#/web/logs/#g' /etc/logrotate.d/apache2 && \
    sed -i 's/Options Indexes/Options /g' /etc/apache2/httpd.conf && \

    apk del tzdata && \
    rm -rf /var/cache/apk/*

# Set Workdir
WORKDIR /web


# Expose volumes
VOLUME /web

EXPOSE 80 443

