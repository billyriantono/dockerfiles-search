FROM registry.centos.org/che-stacks/centos-stack-base

MAINTAINER Madalin Ignisca <madalin.ignisca@yahoo.com>

EXPOSE 8080

LABEL che:server:8080:ref=php che:server:8080:protocol=http

COPY mariadb.repo /etc/yum.repos.d/mariadb.repo

ADD https://getcomposer.org/download/1.6.3/composer.phar /usr/local/bin/composer
ADD https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar /usr/local/bin/wp
ADD https://drupalconsole.com/installer /usr/local/bin/drupal
ADD https://github.com/drush-ops/drush-launcher/releases/download/0.6.0/drush.phar /usr/local/bin/drush

RUN curl -sL https://rpm.nodesource.com/setup_8.x | sudo bash - && \
    sudo yum update -y && \
    sudo yum -y localinstall https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
      https://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    sudo yum-config-manager --enable remi-php72 && \
    sudo yum -y install \
      gcc-c++ make \
      MariaDB-client \
      nano \
      nodejs \
      php-bcmath \
      php-cli \
      php-gd \
      php-gmp \
      php-intl \
      php-json \
      php-mbstring \
      php-mysqlnd \
      php-opcache \
      php-pdo \
      php-process \
      php-snuffleupagus \
      php-sodium \
      php-twig \
      php-xml && \
    sudo yum -y clean all && \
    sudo chmod +xr /usr/local/bin/composer && \
    sudo chmod +xr /usr/local/bin/wp && \
    sudo chmod +xr /usr/local/bin/drupal && \
    sudo chmod +xr /usr/local/bin/drush && \
    cd /tmp && \
    sudo curl -L -o zend-server-php-7.2-common.x86_64.rpm http://repos.zend.com/zend-server/early-access/2018.1/lin/rpm_apache2.4/x86_64/zend-server-php-7.2-common-9.2.0-427.x86_64.rpm && \
    rpm2cpio ./zend-server-php-7.2-common.x86_64.rpm | cpio -iv --to-stdout ./usr/local/zend/lib/debugger/php-7.2.x/ZendDebugger.so > ZendDebugger.so && \
    sudo rm zend-server-php-7.2-common.x86_64.rpm && \
    sudo mv ZendDebugger.so /usr/lib64/php/modules/ && \
    sudo chmod 755 /usr/lib64/php/modules/ZendDebugger.so

COPY my.cnf /etc/my.cnf
COPY php.ini /etc/php.d/99-custom.ini
COPY zenddebugger.ini /etc/php.d/90-zenddebugger.ini
