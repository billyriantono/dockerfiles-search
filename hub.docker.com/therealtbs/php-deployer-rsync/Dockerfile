FROM mwienk/php-deployer

RUN apk --no-cache add rsync

RUN apk --no-cache add libxml2-dev libxslt-dev icu-dev libpng-dev libjpeg-turbo-dev freetype-dev \
    && docker-php-ext-install -j$(nproc) bcmath xml xsl xmlrpc soap intl pdo_mysql \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd
