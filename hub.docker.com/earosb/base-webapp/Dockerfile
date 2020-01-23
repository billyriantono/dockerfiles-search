FROM php:7-fpm

RUN apt-get update && \
	apt-get install -y --no-install-recommends build-essential git zip wget gnupg

RUN curl --silent --show-error https://getcomposer.org/installer | php && \
	mv composer.phar /usr/local/bin/composer

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash && \
	apt-get install -y nodejs

RUN curl -o- -L https://yarnpkg.com/install.sh | bash
