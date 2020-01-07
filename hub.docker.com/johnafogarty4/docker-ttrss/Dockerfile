# PHP-FPM
#
# Version 0.0.4

FROM centos:latest

ENTRYPOINT ["supervisord"]

ADD supervisord.ini /etc/supervisord.d/supervisord.ini
ADD nginx.conf /etc/nginx/conf.d/nginx.conf

VOLUME ["/php"]

EXPOSE 80

RUN /bin/localedef -v -c -i en_US -f UTF-8 en_US.UTF-8;\
    yum -y install epel-release; \
    yum -y install php-gd php-fpm php-mysql php-xml php-soap php-snmp php-pgsql php-odbc php-bcmath php-cli php-common php-enchant php-intl php-mbstring php-pear php-pecl-memcache php-pspell php-recode php-xmlrpc supervisor nginx curl wget ;\
    yum clean all;\
    curl -L https://github.com/kelseyhightower/confd/releases/download/v0.10.0/confd-0.10.0-linux-amd64 -o /usr/bin/confd;\
    chmod +x /usr/bin/confd;\
    echo "cgi.fix_pathinfo = 0;" >> /etc/php.ini;\
    sed -i '/^upload_max_filesize/cupload_max_filesize\ \=\ 64M' /etc/php.ini;\
    sed -i '/^post_max_size/cpost_max_size\ \=\ 64M' /etc/php.ini;\
    sed -i '/^listen = /clisten = 0.0.0.0:9000' /etc/php-fpm.d/www.conf;\
    sed -i '/^listen.allowed_clients/c;listen.allowed_clients =' /etc/php-fpm.d/www.conf;\
    sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g" /etc/php-fpm.conf;\
    sed -i '/^error_log = /cerror_log = /proc/self/fd/2' /etc/php-fpm.conf
