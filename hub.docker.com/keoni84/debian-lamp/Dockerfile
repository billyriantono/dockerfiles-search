FROM debian:stretch-slim
MAINTAINER "keoni84 - https://bitbucket.org/keoni84"

RUN apt-get update && \
groupmod -g 1026 www-data && \
groupadd -g 1020 mysql && \
useradd -u 1026 -g www-data -s /usr/sbin/nologin -M webhost && \
useradd -u 1020 -g mysql -s /usr/sbin/nologin -M mysql && \
usermod -L webhost && usermod -L mysql && \
DEBIAN_FRONTEND=noninteractive apt-get -y install apache2 \
php libapache2-mod-php php-mysql php-common php-curl php-gd php-gmp php-cli php-json php-xml php-pear && \
DEBIAN_FRONTEND=noninteractive apt-get -y install vim-tiny mariadb-server mariadb-client supervisor && \
mkdir /run/mysqld && chown mysql:mysql /run/mysqld && \
apt-get clean && rm -r /var/lib/apt/lists/*

COPY supervisord.conf /etc/supervisor/supervisord.conf
COPY apache.conf /etc/supervisor/conf.d/apache.conf
COPY mariadb.conf /etc/supervisor/conf.d/mariadb.conf

EXPOSE 80

VOLUME ["/var/www/html","/var/lib/mysql"]

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]