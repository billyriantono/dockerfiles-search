FROM centos:7

LABEL maintainer="Eughenio Constantino <eughenio.constantino@gmail.com>"

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# User/Group
ENV MY_USER="apache" \
	MY_GROUP="apache" \
	MY_UID="1000" \
	MY_GID="1000"

ENV MY_LOG_DIR="/var/log/php" \
	MY_LOG_FILE_XDEBUG="/var/log/php/xdebug.log" \
	MY_LOG_FILE_ACC="/var/log/php/www-access.log" \
	MY_LOG_FILE_ERR="/var/log/php/www-error.log" \
	MY_LOG_FILE_SLOW="/var/log/php/www-slow.log" \
	MY_LOG_FILE_FPM_ERR="/var/log/php/php-fpm.err"

RUN \
	groupadd -g ${MY_GID} -r ${MY_GROUP} && \
	adduser -u ${MY_UID} -m -s /bin/bash -g ${MY_GROUP} ${MY_USER}

# Add repository and keys
RUN \
	yum -y update && \
	yum -y install deltarpm && \
	yum -y install epel-release && \
	rpm --import http://rpms.famillecollet.com/RPM-GPG-KEY-remi && \
	rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm && \
	yum-config-manager --enable extras && \
	yum-config-manager --enable epel && \
	yum-config-manager --enable remi && \
	yum-config-manager --disable remi-php55 && \
	yum-config-manager --disable remi-php56 && \
	yum-config-manager --disable remi-php70 && \
	yum-config-manager --disable remi-php71 && \
	rpm -ivh https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm && \
	yum-config-manager --enable pgdg96 && \
	yum clean all && \
	(rm /var/cache/yum/x86_64/7/timedhosts 2>/dev/null || true) && \
	(rm /var/cache/yum/x86_64/7/timedhosts.txt 2>/dev/null || true)

# Install packages
RUN yum -y update && \
	while true; do \
		if yum -y install \
		php \
		php-cli \
		php-fpm \
		\
		php-bcmath \
		php-common \
		php-gd \
		php-gmp \
		php-imap \
		php-intl \
		php-ldap \
		php-magickwand \
		php-mbstring \
		php-mcrypt \
		php-mysqli \
		php-mysqlnd \
		php-opcache \
		php-pdo \
		php-pear \
		php-pgsql \
		php-phalcon2 \
		php-pspell \
		php-recode \
		php-redis \
		php-soap \
		php-tidy \
		php-xml \
		php-xmlrpc \
		\
		php-pecl-amqp \
		php-pecl-apcu \
		php-pecl-imagick \
		php-pecl-memcache \
		php-pecl-memcached \
		php-pecl-mongodb \
		php-pecl-uploadprogress \
		php-pecl-xdebug \
		\
		postfix \
		\
		socat \
		\
		; then \
			break; \
		else \
			yum clean metadata && \
			yum clean all && \
			(rm /var/cache/yum/x86_64/7/timedhosts 2>/dev/null || true) && \
			(rm /var/cache/yum/x86_64/7/timedhosts.txt 2>/dev/null || true) && \
			yum -y update; \
		fi \
	done \
	\
	&& \
	\
	yum -y autoremove && \
	yum clean metadata && \
	yum clean all && \
	(rm /var/cache/yum/x86_64/7/timedhosts 2>/dev/null || true) && \
	(rm /var/cache/yum/x86_64/7/timedhosts.txt 2>/dev/null || true)

RUN yum -y update && \
	yum -y install \
	git \
	openssl \
	openssh && \
	yum -y autoremove && \
	yum clean metadata && \
	yum clean all && \
	(rm /var/cache/yum/x86_64/7/timedhosts 2>/dev/null || true) && \
	(rm /var/cache/yum/x86_64/7/timedhosts.txt 2>/dev/null || true)

RUN \
	curl -sS https://getcomposer.org/installer | php && \
	mv composer.phar /usr/local/bin/composer && \
	composer self-update

RUN \
	localedef -i pt_BR -f UTF-8 pt_BR.UTF-8

COPY \
	./docker-install.sh /
RUN \
	/docker-install.sh

EXPOSE 9000