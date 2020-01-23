FROM million12/centos-supervisor:latest
MAINTAINER Marcin Ryzycki marcin@m12.io, Przemyslaw Ozgo linux@ozgo.info

# - Install Nginx
# - Rename nginx:nginx user/group to www:www
# - Fix permission for /var/lib/nginx which contains Nginx tmp directories (used e.g. during uploading files from upstream servers)
RUN \
  rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm && \
  yum install -y nginx && \

  groupmod --gid 80 --new-name www nginx && \
  usermod --uid 80 --home /data/www --gid 80 --login www --shell /bin/bash --comment www nginx && \

  rm -rf /etc/nginx/*.d /etc/nginx/*_params


RUN \
  yum install -y yum-utils && \

  `# Install PHP 5.6` \
  rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm && \
  yum-config-manager -q --enable remi && \
  yum-config-manager -q --enable remi-php56 && \
  yum install -y php-fpm php-bcmath php-cli php-gd php-intl php-mbstring \
    php-mcrypt php-mysql php-opcache php-pdo && \
  yum install -y --disablerepo=epel php-pecl-redis php-pecl-yaml


RUN \
  yum install -y ruby ruby-devel nodejs npm zlib-devel libpng-devel && \
  yum clean all

ADD docker/images/php/container-files /

RUN yum install git -y
RUN yum install php-devel -y
RUN yes '' | pecl install mongo

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/bin/composer


EXPOSE 80 443
