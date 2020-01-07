FROM alpine:3.4

MAINTAINER Vikas Kumar "vikas@reachvikas.com"

# Let's start
RUN apk update && \
    apk upgrade

# Misc Packages
RUN apk add --no-cache curl git

# Set Timezone
ARG TIMEZONE=Australia/Sydney
RUN apk add --update tzdata && \ 
    cp -v /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \ 
    echo "${TIMEZONE}" > /etc/timezone

# Install Supervisor
ENV PYTHON_VERSION=2.7.14-r0
ENV PY_PIP_VERSION=8.1.2-r0
ENV SUPERVISOR_VERSION=3.3.0

#RUN apk add --no-cache python python-dev py-pip && \
RUN apk add --no-cache -u python=$PYTHON_VERSION py-pip=$PY_PIP_VERSION && \
    pip install supervisor==$SUPERVISOR_VERSION 

# Install PHP
ARG PHP_MEMORY_LIMIT=512M 
ARG PHP_MAX_UPLOAD=50M 
ARG PHP_MAX_FILE_UPLOAD=200
ARG PHP_MAX_POST=100M

RUN apk add --update \ 
php5-mcrypt php5-soap php5-openssl php5-gmp php5-pdo_odbc php5-json php5-dom php5-pdo php5-zip php5-mysql php5-sqlite3 php5-apcu php5-pdo_pgsql php5-bcmath php5-gd php5-xcache php5-odbc php5-pdo_mysql php5-pdo_sqlite php5-gettext php5-xmlreader php5-xmlrpc php5-bz2 php5-memcache php5-xcache php5-mssql php5-iconv php5-pdo_dblib php5-curl php5-ctype php5-fpm -u musl

RUN sed -i \
    -e "s|;*daemonize\s*=\s*yes|daemonize = no|g" \
    -e "s|;*listen\s*=\s*127.0.0.1:9000|listen = 9000|g" \
    -e "s|;*listen\s*=\s*/||g" \
    /etc/php5/php-fpm.conf
RUN sed -i \
    -e "s|;*date.timezone =.*|date.timezone = ${TIMEZONE}|i" \
    -e "s|;*memory_limit =.*|memory_limit = ${PHP_MEMORY_LIMIT}|i" \
    -e "s|;*upload_max_filesize =.*|upload_max_filesize = ${PHP_MAX_UPLOAD}|i" \
    -e "s|;*max_file_uploads =.*|max_file_uploads = ${PHP_MAX_FILE_UPLOAD}|i" \
    -e "s|;*post_max_size =.*|post_max_size = ${PHP_MAX_POST}|i" \
    -e "s|;*cgi.fix_pathinfo=.*|cgi.fix_pathinfo= 0|i" \
    /etc/php5/php.ini

# Install Nginx
RUN apk add nginx ca-certificates
EXPOSE 80 443

ADD files/nginx.conf /etc/nginx/
ADD files/default.conf /etc/nginx/conf.d/
ADD files/info.php  /usr/share/nginx/html/
ADD files/whoami.php /usr/share/nginx/html/

# Clean Up
RUN apk del tzdata && \
    rm -rf /var/cache/apk/*

# Final
ADD files/supervisord.conf /etc/
ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisord.conf"]

# For Swarm Mode (Introduced in v1.12), but not recognised on Docker Hub yet (as on 7/28)
#HEALTHCHECK --interval=5m --timeout=3s --retries=3 CMD curl -f http://localhost/info.php || exit 1
