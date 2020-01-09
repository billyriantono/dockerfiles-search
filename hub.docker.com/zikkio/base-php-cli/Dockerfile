FROM php:7

RUN apt-get -y update && apt-get -y install git-core zip unzip libmcrypt-dev zlib1g-dev

RUN docker-php-ext-install mcrypt mbstring tokenizer pdo_mysql mysqli zip
