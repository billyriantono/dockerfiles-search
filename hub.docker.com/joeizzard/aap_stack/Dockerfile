FROM alpine:latest
MAINTAINER Joe Izzard

ARG BUILD_DATE
ARG VCS_REF

LABEL  org.label-schema.build-date=$BUILD_DATE \
        org.label-schema.schema-version="1.0.0-rc1" \
        org.label-schema.name="AAP Stack" \
        org.label-schema.description="A simple and lightweight Apache PHP server built off Alpine"\
        org.label-schema.version="1.0.1"\
        org.label-schema.vcs-url="https://github.com/JoeIzzard/AAP_Stack"\
        org.label-schema.vcs-ref=$VCS_REF

# Based on the similar build by JCSofts

# Install packages
RUN apk update && apk upgrade && apk add bash \
apache2 \
php7 \
php7-apache2 \
tzdata \
curl \
ca-certificates \
openssl \
openssh \
git \
php7-phar \
php7-json \
php7-iconv \
php7-openssl \
php7-ftp \
php7-xdebug \
php7-mcrypt \
php7-mbstring \
php7-soap \
php7-gmp \
php7-pdo_odbc \
php7-dom \
php7-pdo \
php7-mysqli \
php7-sqlite3 \
php7-pdo_pgsql \
php7-pdo_mysql \
php7-gd \
php7-odbc \
php7-pdo_sqlite \
php7-gettext \
php7-xmlreader \
php7-xmlwriter \
php7-tokenizer \
php7-xmlrpc \
php7-bz2 \
php7-pdo_dblib \
php7-curl \
php7-ctype \
php7-session \
php7-redis \
php7-intl \
php7-apcu \
php7-simplexml

# Create the PID Directory
RUN mkdir /run/apache2

# Expose our Web Ports
EXPOSE 80 443

# Update the config File with basic info
RUN sed -i "s/#LoadModule\ rewrite_module/LoadModule\ rewrite_module/" /etc/apache2/httpd.conf && \
    sed -i "s/#LoadModule\ session_module/LoadModule\ session_module/" /etc/apache2/httpd.conf && \
    sed -i "s/#LoadModule\ session_cookie_module/LoadModule\ session_cookie_module/" /etc/apache2/httpd.conf && \
    sed -i "s/#LoadModule\ session_crypto_module/LoadModule\ session_crypto_module/" /etc/apache2/httpd.conf && \
    sed -i "s/#LoadModule\ deflate_module/LoadModule\ deflate_module/" /etc/apache2/httpd.conf && \
    sed -i "s#^DocumentRoot \".*#DocumentRoot \"/Server/Public\"#g" /etc/apache2/httpd.conf && \
    sed -i "s#/var/www/localhost/htdocs#/Server/Public#" /etc/apache2/httpd.conf && \
    printf "\n<Directory \"/Server/Public\">\n\tAllowOverride All\n</Directory>\n" >> /etc/apache2/httpd.conf

# Build the Project Folder
RUN mkdir -p /Server/Public && chown -R apache:apache /Server/Public && chmod -R 755 /Server/Public

# Copy the Default Project
COPY index.php /Server/Public

# Start Script
COPY start.sh /
RUN chmod +x /start.sh

# Set Entrypoint
ENTRYPOINT [ "/start.sh" ]