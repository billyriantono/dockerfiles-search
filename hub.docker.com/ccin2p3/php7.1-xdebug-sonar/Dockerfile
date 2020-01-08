FROM php:7.1

RUN apt-get update -yqq \
    && apt-get install git wget unzip zlibc zlib1g zlib1g-dev libxml2-dev libssl-dev libicu-dev g++ apt-transport-https sudo gnupg gnupg1 gnupg2 tar libpng-dev -yqq

# install general php extensions
RUN docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install zip \
    && docker-php-ext-install soap \
    && docker-php-ext-install opcache \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && docker-php-ext-install gd
    
# install node
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
RUN apt-get install nodejs npm -yqq

# install xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

# install xsl
RUN apt-get install -y libxslt-dev \
    && docker-php-ext-install xsl
    
# install java
RUN mkdir -p /usr/share/man/man1 \
    && sudo apt-get install default-jre -yqq

# install sonar scanner
RUN wget 'https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-3.2.0.1227-linux.zip' \
    && unzip 'sonar-scanner-cli-3.2.0.1227-linux.zip' \
    && rm 'sonar-scanner-cli-3.2.0.1227-linux.zip' \
    && ln -fs /sonar-scanner-3.2.0.1227-linux /sonar-scanner

RUN sudo apt-get clean
