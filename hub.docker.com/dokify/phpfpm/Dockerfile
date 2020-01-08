FROM php:7.2-fpm

RUN apt-get update && apt-get install -yq --no-install-recommends \
    locales \
    ca-certificates \
    libpng-dev \
    libldb-dev libldap2-dev \
    libmagickwand-dev \
    libmcrypt-dev \
    procps \
    docker.io \
    && apt-get clean && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install gd pdo pdo_mysql ldap mysqli soap zip intl bcmath gettext pcntl\
    && pecl install imagick-beta \
    && docker-php-ext-enable imagick \
    && pecl install -o -f redis \
    && pecl install -o -f mcrypt \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis \
    && sed -i -e 's/# es_ES.UTF-8 UTF-8/es_ES.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# en_GB.UTF-8 UTF-8/en_GB.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# pt_PT.UTF-8 UTF-8/pt_PT.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# fr_FR.UTF-8 UTF-8/fr_FR.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# es_CL.UTF-8 UTF-8/es_CL.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# ca_ES.UTF-8 UTF-8/ca_ES.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# it_IT.UTF-8 UTF-8/it_IT.UTF-8 UTF-8/' /etc/locale.gen \
    && locale-gen

EXPOSE 9000
