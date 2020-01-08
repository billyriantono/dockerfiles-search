FROM php:5.6-cli-stretch

RUN apt-get update; \
	apt-get install -y --no-install-recommends \
	zlib1g-dev \
	libpng-dev \
	git \
	ssh \
	rsync \
	sshpass \
	lftp

RUN	rm -rf /var/lib/apt/lists/*;

RUN docker-php-ext-install zip gd bcmath

# Install composer

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

CMD ["php", "-a"]
