# Set the base image to Centos 7
FROM centos:7

# File Author / Maintainer
MAINTAINER Marc-Jan Barnhoorn

RUN useradd -ms /bin/bash www && \
    yum -y install epel-release && \
    rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm && \
    yum -y makecache fast && \
    yum -y update && \
    yum -y install php-gd php-pdo php-xml php-common php-mysql php-bcmath php-soap php-pear php-imap php-mssql php-mbstring  php-pecl-apcu php-intl php-ldap php-pecl-imagick php-pecl-redis php-mcrypt php-pecl-memcached php-fpm php-pecl-xdebug php-pecl-memcache libssh2 graphviz libssh2-devel php-devel make gcc curl-devel sendmail nsca-client mailx mercurial && \
    pecl install ssh2-0.13 xhprof-beta yar-1.2.5 && \
    yum -y autoremove epel-release php-devel make gcc libssh2-devel curl-devel && \
    yum -y clean all && \
    rm -fr /tmp/* /var/tmp/* /var/cache/yum && \
    echo "extension=ssh2.so" > /etc/php.d/ssh2.ini && \
    printf "xdebug.remote_enable=1\nxdebug.remote_autostart = 1\nxdebug.remote_port=9099\nxdebug.remote_host=host.docker.internal\nxdebug.remote_handler=dbgp\n   xdebug.remote_mode=req" >> /etc/php.d/xdebug.ini && \
    mkdir -p /var/lib/php/session && \
    chown www:www /var/lib/php/session && \
    sed -i -e "s/listen = 127.0.0.1:9000/listen = 9000/g" /etc/php-fpm.d/www.conf && \
    sed -i -e "s/listen.allowed_clients = 127.0.0.1/;listen.allowed_clients = 127.0.0.1/g" /etc/php-fpm.d/www.conf && \
    sed -i -e "s/user = apache/user = www/g" /etc/php-fpm.d/www.conf && \
    sed -i -e "s/group = apache/group = www/g" /etc/php-fpm.d/www.conf && \
    sed -i -e "s/daemonize\s*=\s*yes/daemonize = no/g" /etc/php-fpm.conf && \
    sed -i -e "s/display_errors = Off/display_errors = On/g" /etc/php.ini && \
    sed -i -e "s/error_reporting = E_ALL & ~E_DEPRECATED/error_reporting = E_ALL/g" /etc/php.ini && \
    sed -i -e "s/post_max_size = 8M/post_max_size = 100M/g" /etc/php.ini && \
    sed -i -e "s/upload_max_filesize = 2M/upload_max_filesize = 100M/g" /etc/php.ini && \
    sed -i -e "s/;date.timezone =/date.timezone = Europe\/Amsterdam/g" /etc/php.ini && \
    sed -i -e "s/short_open_tag = Off/short_open_tag = On/g" /etc/php.ini && \
    sed -i -e "s/memory_limit = 128M/memory_limit = -1/g" /etc/php.ini && \
    sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php.ini

ENV TERM xterm

# Set the port to 9000
EXPOSE 9000

COPY docker-entrypoint.sh /

# Set up the command arguments
CMD ["-"]
ENTRYPOINT ["/docker-entrypoint.sh"]
