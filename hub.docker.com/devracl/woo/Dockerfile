FROM wordpress:php5.6-apache

# enable extra Apache modules
RUN a2enmod headers

# install the PHP extensions we need
RUN apt-get update \
  && apt-get install -y libxml2-dev libxslt-dev libgraphicsmagick1-dev graphicsmagick libmcrypt-dev \
  && rm -rf /var/lib/apt/lists/* \
  && docker-php-ext-install json gettext exif calendar soap xsl sockets wddx mysql

# Install PHP mcrypt extension
RUN docker-php-ext-install -j$(nproc) mcrypt

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
    echo 'opcache.memory_consumption=128'; \
    echo 'opcache.interned_strings_buffer=8'; \
    echo 'opcache.max_accelerated_files=4000'; \
    echo 'opcache.revalidate_freq=60'; \
    echo 'opcache.fast_shutdown=1'; \
    echo 'opcache.enable_cli=1'; \
  } > /usr/local/etc/php/conf.d/opcache-recommended.ini

# increase upload size
# see http://php.net/manual/en/ini.core.php
RUN { \
    echo "upload_max_filesize = 95M"; \
    echo "post_max_size = 100M"; \
  } > /usr/local/etc/php/conf.d/uploads.ini

# Set Chile timezone
RUN { \
    echo "date.timezone = \"America/Santiago\""; \
  } > /usr/local/etc/php/conf.d/timezone.ini

# Iron the security of the Docker
RUN { \
    echo "expose_php = Off"; \
    echo "display_startup_errors = off"; \
    echo "display_errors = off"; \
    echo "html_errors = off"; \
    echo "log_errors = On"; \
    echo "error_log = /dev/stderr"; \
    echo "error_reporting = E_ALL"; \
    echo "ignore_repeated_errors = off"; \
    echo "ignore_repeated_source = off"; \
    echo "report_memleaks = on"; \
    echo "track_errors = on"; \
    echo "docref_root = 0"; \
    echo "docref_ext = 0"; \
    echo "log_errors_max_len = 0"; \
  } > /usr/local/etc/php/conf.d/security.ini

RUN { \
    echo "ServerSignature Off"; \
    echo "ServerTokens Prod"; \
    echo "TraceEnable off"; \
  } >> /etc/apache2/apache2.conf

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]
