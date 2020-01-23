FROM wordpress:5.3.0

RUN apt-get update && \
  apt-get install -y --no-install-recommends zlib1g-dev && \
  rm -rf /var/lib/apt/lists/*

RUN pecl install -o -f redis \
  &&  docker-php-ext-enable redis

RUN a2enmod headers

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
