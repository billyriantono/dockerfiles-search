FROM drupal:8.8

ENV COMPOSER_ALLOW_SUPERUSER 1

# Dependencies
RUN apt-get update && apt-get install -y \
		mysql-client \
    	imagemagick \
		unzip \
		git \
		sqlite3 \
	--no-install-recommends && rm -r /var/lib/apt/lists/*

# Set the max upload size.
RUN { \
		echo 'upload_max_filesize = 32M'; \
		echo 'post_max_size = 32M'; \
	} > /usr/local/etc/php/conf.d/upload-filesize.ini

# Optomize container for a low-memory VPS.
RUN { \
		echo 'StartServers 1'; \
		echo 'MinSpareServers 1'; \
	} | tee "$APACHE_CONFDIR/conf-available/low-memory.conf" \
	&& a2enconf low-memory

# Enable Apache modules
RUN a2enmod env headers

# Add Composer
COPY --from=composer:1.9 /usr/bin/composer /usr/bin/composer

# Remove the default Drupal site.
RUN rm -rf /var/www/html
