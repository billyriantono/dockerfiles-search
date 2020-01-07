FROM centos:7

MAINTAINER Valentin Andriès <valentin.andries@gmail.com>

RUN yum -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
RUN yum -y update

RUN yum-config-manager --enable remi-php70

RUN yum -y install \
    php-fpm \
    php-cli \
    php-pdo \
    php-mysql \
    php-xml \
    php-posix \
    php-intl \
    php-pecl-apcu \
    php-pecl-xdebug
RUN yum clean all

RUN set -ex \
	&& cd /etc \
  && sed -e '/include=/d' php-fpm.conf \
  && { \
		echo '[global]'; \
		echo 'include=/etc/php-fpm.d/*.conf'; \
	} >> php-fpm.conf \
	&& { \
		echo '[global]'; \
                echo 'daemonize = no'; \
		echo; \
		echo '[www]'; \
                echo; \
		echo 'clear_env = no'; \
		echo; \
		echo '; Ensure worker stdout and stderr are sent to the main error log.'; \
		echo 'catch_workers_output = yes'; \
	} | tee php-fpm.d/docker.conf

WORKDIR /var/www

EXPOSE 9000
VOLUME ["/etc/php-fpm.d", "/var/log/php-fpm"]

CMD ["php-fpm"]
