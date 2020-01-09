FROM tempbuddy/php:7.0-apache

RUN apt-get update && apt-get install -y --no-install-recommends gnupg && \
    curl https://www.dotdeb.org/dotdeb.gpg | apt-key add - && \
    echo 'deb http://packages.dotdeb.org stretch all' >> /etc/apt/sources.list && \
    echo 'deb-src http://packages.dotdeb.org stretch all' >> /etc/apt/sources.list && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y --no-install-recommends apt-utils libxml2 libxml2-dev libcurl3 libcurl3-dev \
    libmagickwand-dev nodejs yarn git && \
    docker-php-ext-install mysqli pdo_mysql mbstring xml curl soap opcache && \
    pecl install imagick redis xdebug && \
    docker-php-ext-enable imagick && \
    apt-get install -y --no-install-recommends wget && wget https://phar.phpunit.de/phpunit-4.8.35.phar && \
    apt-get remove -y wget && rm -rf /var/lib/apt/lists/* && \
    chmod +x phpunit-4.8.35.phar && \
    cp phpunit-4.8.35.phar /usr/local/bin/phpunit && \
    mv phpunit-4.8.35.phar /usr/local/bin/phpunit.phar && \
    rm -rf /var/lib/apt/lists/*
