FROM centos:6.7

# install prerequisite
RUN yum install -y python-setuptools automake libtool flex bison pkgconfig gcc-c++ boost-devel libevent-devel zliyub-devel python-devel ruby-devel openssl-devel wget make git tar  && yum clean all
RUN easy_install supervisor

# install Nginx
RUN yum install -y epel-release && yum clean all
RUN yum install -y nginx

# install PHP7 with fpm
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
RUN yum install -y php php-devel php-fpm php-opcache php-xml php-pecl-ssh2 php-mcrypt php-mbstring php-pdo php-mysqlnd php-pecl-apcu php-pecl-memcache php-pecl-memcached php-pecl-redis --enablerepo=remi-php72

# web root && log dir
RUN mkdir -p /game/public_html
RUN mkdir -p /game/log/nginx
RUN mkdir -p /game/log/php-fpm
RUN mkdir -p /game/log/supervisord

RUN rm -rf /etc/nginx/nginx.conf
RUN rm -rf /etc/nginx/conf.d/default.conf
RUN rm -rf /etc/php-fpm.d/www.conf

ADD config/nginx.conf /etc/nginx/nginx.conf
ADD config/www.conf /etc/php-fpm.d/www.conf

ADD config/supervisord.conf /etc/supervisord.conf
ADD config/php-fpm.ini /etc/supervisord.d/php-fpm.ini

EXPOSE 80 443 1463

CMD ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]
