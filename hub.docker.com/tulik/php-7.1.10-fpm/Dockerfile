FROM tulik/php-7.1.10

# Install SSL root cert
ADD ssl/symfony.crt /usr/local/share/ca-certificates

RUN apt-get update \
    && apt-get install -y \
	git \
	vim \
	nano \
	zsh \
	telnet \
	bzip2 \
	libbz2-dev \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	libmcrypt-dev \
	libpng-dev \
	libghc-postgresql-libpq-dev \
	php-pear \
	libpq-dev \
	libmemcached-dev \
	libxml2-dev \
	libxslt1-dev \
	imagemagick \
	g++ zlib1g-dev libicu-dev \
    libmcrypt-dev \
	&& docker-php-ext-install mbstring bz2 bcmath zip \
	&& docker-php-ext-configure gd  -with-freetype-dir=/usr/include/ -with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-configure pgsql -with-pgsql=/usr/include/postgresql/ \
	&& docker-php-ext-install -j$(nproc) gd iconv mbstring pdo pgsql pdo_pgsql zip pdo_mysql soap intl xsl opcache bcmath \

    # xdebug
    && pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug

# Install imagick
RUN runtimeRequirements="libmagickwand-6.q16-dev --no-install-recommends" \
    && apt-get update && apt-get install -y ${runtimeRequirements} \
    && ln -s /usr/lib/x86_64-linux-gnu/ImageMagick-6.8.9/bin-Q16/MagickWand-config /usr/bin/ \
    && pecl install imagick-3.4.3RC1 \
    && echo "extension=imagick.so" > /usr/local/etc/php/conf.d/ext-imagick.ini


RUN echo "xdebug.remote_enable=on"  >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_host=10.0.2.2" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.remote_connect_back=On" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.profiler_enable_trigger=On" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/xdebug.ini \
    && echo "memory_limit = 128M" >> /usr/local/etc/php/conf.d/php.ini \
    && echo "upload_max_filesize = 8M" >> /usr/local/etc/php/conf.d/php.ini

# Install bower and gulp
RUN curl -sS "https://getcomposer.org/installer?v=1.5.2" | php \
    && mv composer.phar /usr/bin/composer \
    && update-ca-certificates \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /tmp/pear

CMD ["php-fpm", "-F"]

EXPOSE 9000
