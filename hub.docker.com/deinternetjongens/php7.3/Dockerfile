FROM php:7.3.11

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

RUN apt-get update && apt-get install -my wget gnupg

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y xvfb libgtk-3-dev libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2
RUN apt-get install -y unzip zip libzip-dev
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN apt-get install -qy git curl libmcrypt-dev default-mysql-client
RUN apt-get install -y libpng-dev
RUN apt-get install -y zlib1g-dev
RUN apt-get install -y libpq-dev
RUN docker-php-ext-install mysqli
RUN docker-php-ext-enable mysqli
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install pgsql
RUN docker-php-ext-install pdo_pgsql
RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
RUN docker-php-ext-install bcmath
RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g bower
RUN npm install -g gulp
RUN npm install -g grunt-cli
RUN apt-get install -y ruby-full
RUN gem install compass sass-globbing
RUN apt-get install -y libmagickwand-dev --no-install-recommends
RUN pecl install imagick
RUN docker-php-ext-enable imagick
RUN pecl install pcov
RUN docker-php-ext-enable pcov
RUN cp -f /usr/share/zoneinfo/Europe/Amsterdam /etc/localtime
RUN printf '[PHP]\ndate.timezone = "Europe/Amsterdam"\n' > /usr/local/etc/php/conf.d/tzone.ini
RUN apt-get install -y python-pip python-dev build-essential
RUN pip install --upgrade pip
RUN pip install --upgrade virtualenv
RUN pip install boto3==1.4.7

RUN docker-php-ext-configure pcntl --enable-pcntl
RUN docker-php-ext-install pcntl

RUN apt-get install -y libxml2-dev
RUN docker-php-ext-install soap

RUN apt-get install -y libicu-dev
RUN docker-php-ext-configure intl
RUN docker-php-ext-install intl

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 379CE192D401AB61
RUN echo "deb https://dl.bintray.com/loadimpact/deb stable main" | tee -a /etc/apt/sources.list
RUN apt-get update && apt-get install k6

ADD s3_upload /usr/local/bin
RUN chmod u+x /usr/local/bin/s3_upload
