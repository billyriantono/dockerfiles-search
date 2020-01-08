FROM centos/systemd

ENV ACCEPT_EULA Y
ENV PHP_VERSION php54

ADD https://packages.microsoft.com/config/rhel/7/prod.repo /etc/yum.repos.d/mssql-release.repo

RUN yum -y install epel-release \
https://rpms.remirepo.net/enterprise/remi-release-7.rpm

RUN yum install -y gettext \ 
mediainfo \
openldap-clients \
freetds \
$PHP_VERSION-php


RUN yum install -y $PHP_VERSION-php-{fpm,\
gd,\
intl,\
ldap,\
mbstring,\
mcrypt,\
opcache,\
pdo-dblib,\
soap,\
xml,\
gmp,\
bcmath,\
mhash,\
xsl,\
pear,\
soap,\
tidy,\
pecl-uuid,\
pecl-zip,\
pecl-imagick,\
pecl-apcu}

RUN yum clean all 

RUN ln -s /opt/remi/$PHP_VERSION/root/usr/bin/php /usr/bin/php && \
ln -s /opt/remi/$PHP_VERSION/root/usr/sbin/php-fpm /usr/bin/php-fpm

RUN sed -i -e 's/127.0.0.1/0.0.0.0/g' /opt/remi/$PHP_VERSION/root/etc/php-fpm.d/www.conf

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
php -r "if (hash_file('sha384', 'composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
php composer-setup.php  && \
php -r "unlink('composer-setup.php');" && \
mv composer.phar /usr/bin/composer

EXPOSE 9000

CMD ["php-fpm", "--allow-to-run-as-root", "--nodaemonize"]



