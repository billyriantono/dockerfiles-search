FROM php:7.2.15-apache-stretch

RUN apt-get update && \
	apt-get install -y --no-install-recommends mysql-client \
	zlib1g-dev \
	libpng-dev \
	git \
	ssh \
	rsync \
	libicu-dev \
	g++ \
	wget

RUN	rm -rf /var/lib/apt/lists/*;

RUN docker-php-ext-install zip && \
    docker-php-ext-install gd && \
    docker-php-ext-install mysqli && \
    docker-php-ext-install pdo && \
    docker-php-ext-install pdo_mysql  && \
    docker-php-ext-install mbstring && \
    docker-php-ext-configure intl && \
    docker-php-ext-install intl && \
    docker-php-ext-install sockets && \
    docker-php-ext-install bcmath && \
    docker-php-ext-configure bcmath --enable-bcmath

RUN a2enmod rewrite
RUN a2enmod ssl

# Install composer

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Install WP-CLI for wordpress

RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN chmod +x wp-cli.phar
RUN mv wp-cli.phar /usr/local/bin/wp

CMD ["php", "-a"]
