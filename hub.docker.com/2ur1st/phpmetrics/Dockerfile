FROM php:7.1.3-alpine

MAINTAINER herloct <herloct@gmail.com>

ENV PHP_METRICS_VERSION=1.10.0

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
RUN curl -sL https://github.com/phpmetrics/PhpMetrics/archive/v${PHP_METRICS_VERSION}.tar.gz | tar xz

WORKDIR /PhpMetrics-${PHP_METRICS_VERSION}
RUN composer install \
	&& ln -s /PhpMetrics-${PHP_METRICS_VERSION}/bin/phpmetrics /usr/local/bin/phpmetrics \
	&& rm -rf /var/cache/apk/* /var/tmp/* /tmp/*

VOLUME ["/project"]
WORKDIR /project

ENTRYPOINT ["phpmetrics"]
CMD ["--version"]
