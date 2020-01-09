FROM centos:7

RUN yum -y install epel-release yum-utils \
	&& rpm -ivh http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
	&& yum-config-manager --enable remi-php71 \
	&& yum -y install composer \
		libev \
		libevent \
		php-pecl-amqp \
		php-pecl-ev \
		php-pecl-event \
		php-pecl-libsodium \
		php-bcmath \
		php-cli \
		php-common \
		php-devel \
		php-fedora-autoloader \
		php-fpm \
		php-gd \
		php-gmp \
		php-intl \
		php-json \
		php-mbstring \
		php-mcrypt \
		phpMyAdmin \
		php-mysqlnd \
		php-pdo \
		php-pear \
		php-pecl-igbinary \
		php-pecl-redis \
		php-pecl-zip \
		php-php-gettext \
		php-phpseclib \
		php-process \
		php-recode \
		php-soap \
		php-symfony-class-loader \
		php-symfony-common \
		php-tcpdf-dejavu-sans-fonts \
		php-tidy \
		php-udan11-sql-parser \
		php-xml \
		php-pecl-memcached \
	&& yum clean all \
	&& rm -rf /var/cache/yum


