FROM docker.io/library/centos:centos7
MAINTAINER smoulhac <smoulhac.prestataire@voyages-sncf.com>

RUN echo "ADD PACKAGE" \
    && yum -y install wget.x86_64 \
    && wget http://repo.mysql.com/mysql-community-release-el7-7.noarch.rpm \
    && rpm -ivh mysql-community-release-el7-7.noarch.rpm \
    && yum -y update \
    && yum -y install -y libcurl4-openssl-dev openssl libicu-dev git \
    && mkdir /tmp/dd-security/ /tmp/dd-security/app /tmp/dd-security/app/cache /tmp/dd-security/app/logs \
    && chmod 777 /tmp/dd-security/ -R

RUN echo "PHP DEPLOY" \
    && rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm \
    && yum -y install php56w php56w-mysql php56w-bcmath php56w-cli php56w-intl php56w-gd php56w-xml \
    && yum -y install  make gcc libssh2 php56w-devel php-pear libssh2-devel \
    && pecl install -f ssh2 \
    && echo 'extension=ssh2.so' | tee /etc/php.d/ext-ssh2.ini > /dev/null \
    && rm /etc/php.ini

ADD ./php.ini /etc

RUN echo "APACHE DEPLOY" \
    && yum -y install httpd \
    && rm /etc/httpd/conf.d/welcome.conf \
    && echo "IncludeOptional vhosts/enabled/*.conf" >> /etc/httpd/conf/httpd.conf \
    && mkdir /etc/httpd/vhosts /etc/httpd/vhosts/enabled

ADD ./dd_ihm.conf /etc/httpd/vhosts/enabled/dd_ihm.conf

VOLUME /var/www/html
VOLUME /etc/httpd/vhosts/
VOLUME /etc/httpd/conf.modules.d
VOLUME /etc/php.d
VOLUME /tmp

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/docker-entrypoint.sh /entrypoint.sh # backwards compat
ENTRYPOINT ["docker-entrypoint.sh"]