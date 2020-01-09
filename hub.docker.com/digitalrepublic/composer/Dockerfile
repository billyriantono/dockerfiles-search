FROM alpine:3

COPY scripts /scripts

RUN /scripts/install-packages.sh \
	&& rm -rf /scripts

# Adapted from
# https://github.com/composer/docker/blob/0303cc2362774266be5845e9f2487312fda8b7f5/1.4/Dockerfile
RUN apk --no-cache add curl git subversion openssh openssl mercurial tini bash

RUN echo "memory_limit=-1" > "/etc/php7/conf.d/memory-limit.ini" \
	&& echo "date.timezone=${PHP_TIMEZONE:-UTC}" > "/etc/php7/conf.d/date_timezone.ini"

ENV PATH "/composer/vendor/bin:$PATH"
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV COMPOSER_VERSION 1.5.0

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('sha384', 'composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"

COPY composer/docker-entrypoint /usr/local/bin/

# Prestissimo speeds up composer install/update massively
RUN composer global require hirak/prestissimo

ARG oauth_token 

RUN composer config --global github-oauth.github.com $oauth_token

WORKDIR /app

ENTRYPOINT ["docker-entrypoint"]

CMD ["composer"]