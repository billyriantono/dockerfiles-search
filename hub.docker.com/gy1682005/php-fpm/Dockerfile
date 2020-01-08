FROM centos:7
MAINTAINER tanghao <gy1682005@qq.com>

RUN yum install -y epel-release &&\
    yum install -y https://mirror.webtatic.com/yum/el7/webtatic-release.rpm &&\
    yum install -y supervisor \
        php70w php70w-common php70w-cli php70w-fpm php70w-process php70w-tidy php70w-xml php70w-xmlrpc \
        php70w-bcmath php70w-mbstring php70w-mcrypt php70w-gd php70w-pdo php70w-mysqlnd php70w-imap php70w-opcache \
        php70w-pear php70w-pecl-apcu php70w-pecl-geoip php70w-pecl-igbinary php70w-pecl-imagick php70w-pecl-memcached php70w-pecl-redis &&\
    yum clean all

COPY config/supervisord.conf /etc/
COPY config/php-fpm.ini /etc/supervisord.d/

WORKDIR /var/www/html
EXPOSE 9000

CMD ["supervisord", "-c", "/etc/supervisord.conf"]