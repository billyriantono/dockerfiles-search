FROM centos:7

ARG PHP=php72w
ARG MARIADB_VERSION=10.4

RUN set -xe \
# Install packages
&&  echo -e "[mariadb]\\nname = MariaDB" > /etc/yum.repos.d/mariadb.repo \
&&  echo -e "baseurl = http://yum.mariadb.org/${MARIADB_VERSION}/centos7-amd64" >> /etc/yum.repos.d/mariadb.repo \
&&  echo -e "gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB\\ngpgcheck=1"  >> /etc/yum.repos.d/mariadb.repo \
&&  yum update -y \
&&  yum install -y \
        epel-release \
&&  rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm \
&&  yum install -y \
        gcc \
        httpd \
        libmcrypt-devel \
        mariadb-client \
        mariadb-server \    
        mod_${PHP} \
        python-pip \
        ${PHP}-bcmath \
        ${PHP}-ctype \
        ${PHP}-curl \
        ${PHP}-devel \
        ${PHP}-dom \
        ${PHP}-gd \
        ${PHP}-hash \
        ${PHP}-intl \
        ${PHP}-json \
        ${PHP}-libxml \
        ${PHP}-mbstring \
        ${PHP}-mysql \
        ${PHP}-opcache \
        ${PHP}-openssl \
        ${PHP}-pear \
        ${PHP}-posix \
        ${PHP}-soap \
        ${PHP}-spl \
        ${PHP}-tidy \
        ${PHP}-xmlrpc \
        ${PHP}-xsl \
        ${PHP}-zip \
&&  pecl install mcrypt-1.0.2 \
&&  echo "extension=mcrypt.so" > /etc/php.d/mcrypt.ini \
&&  pip install --upgrade pip \
&&  pip install supervisor \
&&  mkdir -p /var/run/supervisor
# &&  mysql -u root -e "SET SQL_MODE=''; GRANT ALL ON *.* TO root@'%' IDENTIFIED BY '';"

# Install configs
COPY configs/ /

ENTRYPOINT [ "docker-entrypoint.sh" ]
CMD [ "/usr/bin/supervisord", "-n" ]