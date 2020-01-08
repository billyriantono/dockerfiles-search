FROM php:7.1-cli
MAINTAINER EasycomLab <easycomlab@easycom.digital>

# =========================================
# RUN update
# =========================================
RUN apt-get update

# =========================================
# Install dependencies
# =========================================
RUN apt-get install -y git zlib1g-dev wget

# =========================================
# Install php required extensions
# =========================================
RUN docker-php-ext-install zip

# Get composer installed to /usr/local/bin/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Get phpmd installed to /usr/local/bin/phpmd
RUN wget http://static.phpmd.org/php/latest/phpmd.phar -O phpmd && chmod a+x phpmd && mv phpmd /usr/local/bin/phpmd

# Get php-cs-fixer installed to /usr/local/bin/php-cs-fixer
RUN wget https://cs.sensiolabs.org/download/php-cs-fixer-v2.phar -O php-cs-fixer && chmod a+x php-cs-fixer && mv php-cs-fixer /usr/local/bin/php-cs-fixer

# Get php-cs installed to /usr/local/bin/phpcs
RUN wget https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar -O phpcs && chmod a+x phpcs && mv phpcs /usr/local/bin/phpcs
