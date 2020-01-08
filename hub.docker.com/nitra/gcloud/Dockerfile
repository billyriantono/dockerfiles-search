FROM nitra/gcloud:dc

# Docker-compose, PHP, static analyzers install
RUN apk add --no-cache php7 php7-phar php7-json php7-openssl php7-zlib php7-ctype php7-iconv php7-mbstring php7-tokenizer php7-xml php7-simplexml php7-dom \   
    && wget https://getcomposer.org/installer  -O - -q | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require friendsofphp/php-cs-fixer \
    && composer global require --dev jakub-onderka/php-parallel-lint \
    && composer global require --dev phpmd/phpmd \
    && composer global require sensiolabs/security-checker