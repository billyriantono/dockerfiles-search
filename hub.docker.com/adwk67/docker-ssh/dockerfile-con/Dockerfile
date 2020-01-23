FROM php:7.1-cli-jessie

ENV DRUSH_VERSION 8.1.15

RUN apt-get update \
	&& apt-get install -y mysql-client postgresql-client libpq-dev libfreetype6-dev \
    libjpeg62-turbo-dev libmcrypt-dev libpng12-dev libbz2-dev libxslt-dev \
    unzip wget --no-install-recommends \
	&& rm -r /var/lib/apt/lists/* \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install gd opcache mbstring mysqli pdo pdo_mysql pdo_pgsql pgsql bcmath mcrypt zip bz2 mbstring pcntl xsl \
	&& curl -fsSL -o /usr/local/bin/drush "https://github.com/drush-ops/drush/releases/download/$DRUSH_VERSION/drush.phar" \
	&& chmod +x /usr/local/bin/drush \
	&& drush @none dl registry_rebuild-7.x \
	&& drush cc drush

VOLUME ["/app"]
WORKDIR /app

ENTRYPOINT ["drush"]