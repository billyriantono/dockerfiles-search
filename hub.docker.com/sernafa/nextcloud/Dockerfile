FROM nextcloud:fpm

RUN apt-get update && apt-get install -y libgmp3-dev libbz2-dev bzip2 libmagickcore-6.q16-3-extra && rm -rf /var/lib/apt/lists/* && docker-php-ext-install gmp bz2

