FROM php:7.2-apache

LABEL authors https://www.oda-alexandre.com/

ENV USER erp
ENV PORTS 80
ENV DEBIAN_FRONTEND noninteractive

ENV	PHP_INI_DATE_TIMEZONE UTC
ENV	PHP_MEMORY_LIMIT 256M
ENV	PHP_MAX_UPLOAD 20M
ENV	PHP_MAX_EXECUTION_TIME 300

RUN echo -e '\033[36;1m ******* INSTALL PACKAGES ******** \033[0m' && \
apt update && apt install -y --no-install-recommends \
sudo \
rsync \
sendmail \
libcurl4-openssl-dev \
libfreetype6-dev \
libjpeg-dev \
libldap2-dev \
libmagickcore-dev \
libmagickwand-dev \
libmcrypt-dev \
libpng-dev \
libpq-dev \
libxml2-dev \
unzip && \
apt install -f -y

RUN echo -e '\033[36;1m ******* ADD USER ******** \033[0m' && \
useradd -d /home/${USER} -m ${USER} && \
passwd -d ${USER} && \
adduser ${USER} sudo

RUN echo -e '\033[36;1m ******* INSTALL APP ******** \033[0m'
COPY ./includes/scripts/  /var/www/scripts
COPY ./includes/htdocs/  /var/www/html

RUN echo -e '\033[36;1m ******* CREATE & SECURISE WORKING SPACE ******** \033[0m' && \
mkdir -p /var/www/documents && \
chown -R www-data:www-data /var/www && \
chmod +x /var/www/scripts/*

RUN echo -e '\033[36;1m ******* CONFIG MULTIARCH ******** \033[0m' && \
debMultiarch="$(dpkg-architecture --query DEB_BUILD_MULTIARCH)" && \
docker-php-ext-configure ldap --with-libdir="lib/$debMultiarch" && \
docker-php-ext-configure gd --with-freetype-dir=/usr --with-png-dir=/usr --with-jpeg-dir=/usr

RUN echo -e '\033[36;1m ******* INSTALL PACKAGES PHP ******** \033[0m' && \
docker-php-ext-install \
calendar \
gd \
ldap \
mbstring \
mysqli \
pdo \
pdo_mysql \
pdo_pgsql \
pgsql \
soap \
zip \
intl

RUN echo -e '\033[36;1m ******* INSTALL IMAGICK ******** \033[0m' && \
pecl install imagick && \
docker-php-ext-enable imagick

RUN echo -e '\033[36;1m ******* CLEANING ******** \033[0m' && \
apt-get --purge autoremove -y && \
apt-get autoclean -y && \
rm /etc/apt/sources.list && \
rm -rf /var/cache/apt/archives/* && \
rm -rf /var/lib/apt/lists/*

RUN echo -e '\033[36;1m ******* SELECT USER ******** \033[0m'
USER ${USER}

RUN echo -e '\033[36;1m ******* SELECT WORKING SPACE ******** \033[0m'
WORKDIR /var/www/html

RUN echo -e '\033[36;1m ******* SHARING VOLUME ******** \033[0m'
VOLUME /var/www/html /var/www/documents /var/www/scripts

RUN echo -e '\033[36;1m ******* OPENING PORTS ******** \033[0m'
EXPOSE ${PORTS}

RUN echo -e '\033[36;1m ******* CONTAINER START COMMAND ******** \033[0m'
CMD sudo apache2-foreground \