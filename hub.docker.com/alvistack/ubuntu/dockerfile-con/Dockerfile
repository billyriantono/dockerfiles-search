FROM centos

LABEL Maintainer="Jindřich Káňa <jindrich.kana@gmail.com>"
LABEL Vendor="ELOS Technologies, s.r.o."

RUN     yum -y --setopt=tsflags=nodocs update \
        && yum --setopt=tsflags=nodocs -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
        && yum --setopt=tsflags=nodocs -y install \
        gcc \
        gcc-c++ \
        httpd \
        mod_ssl \
	mariadb \
        php \
        php-cli \
        php-devel \
        php-mysql \
        php-pdo \
        php-mbstring \
        php-soap \
        php-gd \
        php-xml \
        php-pecl-apcu \
        libXrender fontconfig libXext urw-fonts \
        && yum clean all \
        && rm -rf /var/cache/yum

ADD https://raw.githubusercontent.com/albereinstein/demo/master/reviews.html /var/www/html
ADD https://raw.githubusercontent.com/albereinstein/demo/master/addreview.php /var/www/html
ADD https://raw.githubusercontent.com/albereinstein/demo/master/info.php /var/www/html

ENV SERVER_NAME="localhost"

RUN find /var/www/html/ -type d -exec chmod 755 {} \; \
    && find /var/www/html/ -type f -exec chmod 644 {} \; \
    && sed -i 's/80/8080/g' /etc/httpd/conf/httpd.conf \
    && sed -i 's/DirectoryIndex\ index\.html/DirectoryIndex\ index\.html\ index\.php/g' /etc/httpd/conf/httpd.conf \
    && sed -i '/\<IfModule\ mime\_module\>/a AddType\ application\/x\-httpd\-php\ \.php' /etc/httpd/conf/httpd.conf \
    && sed -i '/\#ServerName\ www\.example\.com\:8080/a ServerName\ \$\{SERVER_NAME\}' /etc/httpd/conf/httpd.conf \
    && echo 'extension=mysqli.so' >> /etc/php.ini \
    && rm -rf /etc/httpd/conf.d/* \
    && chown -R apache: /var/log/httpd /run/httpd \
    && ln -sf /dev/stdout /var/log/httpd/access_log \
    && ln -sf /dev/stderr /var/log/httpd/error_log 

EXPOSE 8080

USER apache

#ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
