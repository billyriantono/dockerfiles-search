FROM drupal:7
RUN apt-get update && apt-get install -y mysql-client libmemcached-dev zlib1g-dev \
	&& pecl install memcached-3.0.4 \
	&& docker-php-ext-enable memcached \
	&& apt-get clean \
	&& rm -r /var/lib/apt/lists/*
RUN echo '[PHP]\n\
      max_execution_time = 120\n\
      max_input_time = 120\n\
      max_input_vars = 5000\n\
      memory_limit = 512M\n\
      post_max_size = 100M\n\
      file_uploads = On\n\
      upload_max_filesize = 100M\n\
      max_file_uploads = 20\n\
[Date]\n\
      date.timezone =America/New_York\n\
      date.default_latitude = 39.98\n\
      date.default_longitude = -76.94\n' >> $PHP_INI_DIR/php.ini
COPY ./favicon.ico /var/www/html/favicon.ico
RUN php -r "readfile('https://github.com/drush-ops/drush/releases/download/8.1.17/drush.phar');" > drush \
  && chmod +x drush \
  && mv drush /usr/local/bin
