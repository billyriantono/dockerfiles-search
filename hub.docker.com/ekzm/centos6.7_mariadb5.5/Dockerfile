FROM centos:6.7

RUN echo $'[mariadb]\n\ 
name = MariaDB\n\
baseurl = http://yum.mariadb.org/5.5/centos6-amd64\n\
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB\n\
gpgcheck=1\n'\
>> /etc/yum.repos.d/MariaDB.repo

RUN yum update -y \
  && yum install make -y \
  && yum install gcc -y \
  && yum install gcc-c++ -y \
  && yum install autoconf -y \
  && yum install automake -y \
  && yum install git -y \
  && yum install mariadb-server -y \
  && yum install php -y \
  && yum install php-mysql -y \
  && yum install php-pdo -y \
  && yum install php-xml -y \
  && yum install php-devel -y \
  && yum install php-pear -y \
  && yum install php-mbstring -y \
  && yum install expect -y \
  && yum clean all

# Setup Xdebug
RUN pecl install xdebug-2.2.7

ENV PHP_INI_DIR="/etc"
ENV PHP_TIMEZONE="Asia/Tokyo"

# Memory Limit
RUN echo "memory_limit=-1" > $PHP_INI_DIR/php.d/memory-limit.ini

# Time Zone
RUN echo "date.timezone=${PHP_TIMEZONE:-UTC}" > $PHP_INI_DIR/php.d/date_timezone.ini

# Xdebug
RUN echo "zend_extension=/usr/lib64/php/modules/xdebug.so" > $PHP_INI_DIR/php.d/xdebug.ini

# Register the COMPOSER_HOME environment variable
ENV COMPOSER_HOME /composer

# Add global binary directory to PATH and make sure to re-export it
ENV PATH /composer/vendor/bin:$PATH

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER 1

# Setup the Composer installer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
  && php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer

COPY run-mysql.sh /run-mysql.sh
