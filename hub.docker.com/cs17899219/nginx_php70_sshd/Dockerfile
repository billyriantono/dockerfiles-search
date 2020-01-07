FROM ubuntu:14.04
MAINTAINER Joseph zhou "joseph.zhou@gmail.com"

# Keep upstart from complaining
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -sf /bin/true /sbin/initctl

# update source
#RUN sudo sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list
#RUN sudo sed -i 's/archive.ubuntu.com/mirrors.aliyuncs.com/g' /etc_nginx/apt/sources.list
#RUN sudo sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc_nginx/apt/sources.list
#Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update --fix-missing

RUN apt-get install -y language-pack-en-base python-software-properties software-properties-common supervisor rsync tree vim nginx openssl libpcre3 libpcre3-dev
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN ln -s /usr/lib/x86_64-linux-gnu/libssl.so  /usr/lib
RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php -y
RUN apt-get update --fix-missing

RUN apt-get -y install php7.0-dev php7.0-fpm php7.0-gd php7.0-xml php7.0-mysql php7.0-mcrypt php7.0-curl php7.0-mbstring
RUN tree /etc/php
RUN sed -i '/daemonize /c \
daemonize = no' /etc/php/7.0/fpm/php-fpm.conf

#RUN sed -i '/^listen /c \
#listen = 0.0.0.0:9000' /etc/php/7.0/fpm/pool.d/www.conf
#RUN sed -i 's/^listen.allowed_clients/;listen.allowed_clients/' /etc/php/7.0/fpm/pool.d/www.conf
RUN sed -i "s/;date.timezone =.*/date.timezone = Asia\/Shanghai/" /etc/php/7.0/fpm/php.ini
RUN sed -i "s/;date.timezone =.*/date.timezone = Asia\/Shanghai/" /etc/php/7.0/cli/php.ini
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/" /etc/php/7.0/fpm/php.ini
RUN pecl install mongodb
RUN echo "extension=mongodb.so" >> /etc/php/7.0/fpm/php.ini
RUN echo "extension=mongodb.so" >> /etc/php/7.0/cli/php.ini
RUN pecl install redis
RUN echo "extension=redis.so" >> /etc/php/7.0/fpm/php.ini
RUN echo "extension=redis.so" >> /etc/php/7.0/cli/php.ini
RUN pecl install xdebug
RUN echo "\n[Xdebug]\n;zend_extension=xdebug.so\n;xdebug.remote_enable=1\nxdebug.remote_connect_back=0\nxdebug.remote_host=127.0.0.1" >> /etc/php/7.0/fpm/php.ini
RUN echo "\n[Xdebug]\n;zend_extension=xdebug.so\n;xdebug.remote_enable=1\nxdebug.remote_connect_back=0\nxdebug.remote_host=127.0.0.1" >> /etc/php/7.0/cli/php.ini

RUN mkdir -p /run/php
RUN mkdir -p /var/log/supervisor
RUN echo "[supervisord]\nnodaemon=true\n[program:php-fpm]\ncommand=php-fpm7.0\n[program:nginx]\ncommand=nginx\n[program:sshd]\ncommand=/usr/sbin/sshd -D" > /etc/supervisor/conf.d/supervisord.conf
RUN echo "Asia/Shanghai" > /etc/timezone;
RUN dpkg-reconfigure tzdata

RUN apt-get install -y openssh-server
RUN mkdir -p /var/run/sshd
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin without-password/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/^#PasswordAuthentication\s+.*/PasswordAuthentication no/' /etc/ssh/sshd_config

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22 80 443

CMD ["/usr/bin/supervisord"]
