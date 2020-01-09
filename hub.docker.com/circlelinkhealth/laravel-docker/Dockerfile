FROM php:7.2

# this image adds additional software to default php image
# to allow ci tests run faster
#
# additional software :
#  - php extentions : mcrypt zip pdo_mysql opcache gd pcntl exif
#  - composer
#  - nodejs/npm
#  - autotools (automake/autoconf)
#  - git/wget/curl etc


MAINTAINER Michalis Antoniou <mantoniou@circlelinkhealth.com>

RUN apt-get update -yqq \
		&& apt-get install -y curl \
		&& curl -sL https://deb.nodesource.com/setup_11.x | bash - \
		&& buildDeps=" \
			libz-dev  \
			libpq-dev  \
			libjpeg-dev  \
			libpng-dev  \
			libfreetype6-dev  \
			libmcrypt-dev \
        " \
		&& apt-get install -y git zip unzip bzip2 wget tar less \
			nodejs \
			libtool \
			automake autoconf \
			fontconfig libicu-dev libfontconfig1 \
			libsqlite3-dev \
			openssh-client \
			$buildDeps --no-install-recommends \
        && rm -r /var/lib/apt/lists/* \
        \
		&& docker-php-ext-install gd zip pdo_mysql opcache pcntl exif bcmath \
		&& docker-php-ext-configure gd  \
				--enable-gd-native-ttf  \
				--with-jpeg-dir=/usr/lib  \
				--with-libzip \
				--with-freetype-dir=/usr/include/freetype2 \
        && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
		&& rm -rf /tmp/pear \
        && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $buildDeps \
        && mkdir ~/.ssh \
        && ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts

