FROM chialab/php:7.3-apache

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y libxslt-dev \
    && docker-php-ext-install -j$(nproc) xsl \
    && apt-get purge -y --auto-remove libxslt-dev \
    && rm -r /var/lib/apt/lists/*


