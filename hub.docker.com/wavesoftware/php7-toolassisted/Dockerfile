FROM quay.io/wavesoftware/php7
RUN apt-get update && apt-get install -y \
    imagemagick \
    ffmpeg \
    libreoffice \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*
RUN pecl install imagick-3.4.4
RUN docker-php-ext-enable imagick
