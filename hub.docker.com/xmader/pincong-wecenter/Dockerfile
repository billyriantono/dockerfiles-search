FROM alpine:3.9

ENV TERM xterm

RUN apk update && \ 
    apk upgrade && \ 
    apk add --update \ 
        openssl \ 
        php7-mcrypt \ 
        php7-soap \ 
        php7-openssl \ 
        php7-gmp \ 
    #   php7-pdo_odbc \ 
        php7-json \ 
        php7-dom \ 
        php7-pdo \ 
        php7-zip \ 
        php7-mysqli \ 
    #   php7-sqlite3 \ 
    #   php7-pdo_pgsql \ 
        php7-bcmath \ 
        php7-gd \ 
    #   php7-odbc \ 
        php7-pdo_mysql \ 
    #   php7-pdo_sqlite \ 
        php7-gettext \ 
        php7-xmlreader \ 
        php7-xmlrpc \ 
        php7-bz2 \ 
        php7-iconv \ 
    #   php7-pdo_dblib \ 
        php7-curl \
        php7-session \
        php7-fpm \
        php7-ctype \
        mysql \
        mysql-client \
        bash \
        unzip \
        wget \
        nginx \
        ca-certificates && \
    apk add -u musl && \
    mkdir -p /var/lib/mysql && \
    mkdir -p /etc/mysql/conf.d && \
    mkdir -p /etc/nginx/conf.d && \
    mkdir -p /var/run/mysql/ && \
    rm -f /var/cache/apk/*

ADD files/nginx.conf /etc/nginx/
ADD files/php-fpm.conf /etc/php/
ADD files/my.cnf /etc/mysql/
ADD files/default.conf /etc/nginx/conf.d/
ADD files/run.sh /
ADD files/database.php /tmp/
RUN chmod +x /run.sh

ENV GITHUB_USERNAME pincong
ENV GITHUB_REPO pincong-wecenter
ENV SOURCE_BRANCH master

EXPOSE 80
EXPOSE 3306
WORKDIR /data/htdocs
VOLUME ["/data/htdocs", "/data/logs", "/var/lib/mysql", "/etc/mysql/conf.d/"]
CMD ["/run.sh"]
