FROM php:7.2-fpm
MAINTAINER EasycomLab <easycomlab@easycom.digital>

# =========================================
# RUN update
# =========================================
RUN apt-get update

# =========================================
# Install dependencies
# =========================================
RUN apt-get install -y \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libxslt1-dev \
    libzip-dev \
    pdftk \
    sudo \
    libmagickwand-dev \
    libmagickcore-dev \
    apt-transport-https

# =========================================
# Install tools
# =========================================
RUN apt-get install -y \
    nano \
    vim \
    htop \
    iptraf \
    ssmtp \
    openssl \
    git

# =========================================
# Configure the GD library
# =========================================
RUN docker-php-ext-configure \
    gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# =========================================
# Install php required extensions
# =========================================
RUN docker-php-ext-install \
  dom \
  gd \
  intl \
  mbstring \
  pdo_mysql \
  xsl \
  zip \
  soap \
  bcmath \
  mysqli \
  exif

# =========================================
# Install Xdebug (but don't enable)
# =========================================
RUN pecl install xdebug-2.7.0beta1

# =========================================
# Install apcu
# =========================================
RUN pecl install -f apcu

# =========================================
# Install imagick
# =========================================
RUN pecl install -f imagick

# =========================================
# Set ENV variables
# =========================================
ENV PHP_MEMORY_LIMIT 2G
ENV PHP_XDEBUG_ENABLED false
ENV DEBUG false
ENV UPLOAD_MAX_FILESIZE 64M
ENV PROJECT_ROOT /var/www/htdocs

# =========================================
# Create easycom user
# =========================================
RUN openssl rand -base64 32 > ./.pass \
	&& useradd -ms /bin/bash --password='$(cat ./.pass)' easycom \
	&& echo "$(cat ./.pass)\n$(cat ./.pass)\n" | passwd easycom \
	&& mv ./.pass /home/easycom/ \
	&& chown -Rf easycom:easycom /home/easycom
ADD ./bashrc.easycom /home/easycom/.bashrc

# =========================================
# PHP Configuration
# =========================================
ADD etc/php-xdebug.ini /usr/local/etc/php/conf.d/zz-xdebug-settings.ini
ADD etc/php-fpm.conf /usr/local/etc/
ADD etc/php-fpm.ini /usr/local/etc/php/conf.d/zz-custom.ini

RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

# =========================================
# Configure sendmail
# =========================================

# It permits to send email with custom sender address
RUN sed -i s,#FromLineOverride=YES,FromLineOverride=YES, /etc/ssmtp/ssmtp.conf

# =========================================
# Set entrypoint
# =========================================
ADD docker-entrypoint.sh /docker-entrypoint.sh
RUN ["chmod", "+x", "/docker-entrypoint.sh"]
ENTRYPOINT ["/docker-entrypoint.sh"]

WORKDIR $PROJECT_ROOT

CMD ["php-fpm", "-F"]
