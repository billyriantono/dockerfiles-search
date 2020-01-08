FROM php:5.6.38

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

RUN apt-get update && apt-get install -my wget gnupg libxml2-dev

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get install -y unzip zip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN apt-get install -qy git curl libmcrypt-dev mysql-client
RUN apt-get install -y libpng-dev libssl-dev zlib1g-dev
RUN docker-php-ext-install opcache
RUN docker-php-ext-install pdo
RUN docker-php-ext-install xml
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install calendar
RUN docker-php-ext-install ctype
RUN docker-php-ext-install dom
RUN docker-php-ext-install exif
RUN docker-php-ext-install fileinfo
RUN docker-php-ext-install ftp
RUN docker-php-ext-install gd
RUN docker-php-ext-install gettext
RUN docker-php-ext-install iconv
RUN docker-php-ext-install intl
RUN docker-php-ext-install json
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install mysql
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install posix
RUN docker-php-ext-install shmop
RUN docker-php-ext-install simplexml
RUN docker-php-ext-install sockets
RUN docker-php-ext-install sysvmsg
RUN docker-php-ext-install sysvsem
RUN docker-php-ext-install sysvshm
RUN docker-php-ext-install tokenizer
RUN docker-php-ext-install wddx
RUN docker-php-ext-install xmlreader
RUN docker-php-ext-install xmlwriter
RUN docker-php-ext-install zip
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g bower
RUN npm install -g gulp
RUN apt-get install -y libmagickwand-dev --no-install-recommends
RUN pecl install imagick
RUN docker-php-ext-enable imagick
RUN pecl install xdebug-2.5.5
RUN docker-php-ext-enable xdebug
RUN apt-get install -y python-pip python-dev build-essential
RUN pip install --upgrade pip
RUN pip install --upgrade virtualenv
RUN pip install boto3==1.4.7

RUN apt-get install -y libxml2-dev
RUN docker-php-ext-install soap

RUN echo "memory_limit = -1;\n" > /usr/local/etc/php/conf.d/custom.ini

ADD s3_upload /usr/local/bin
RUN chmod u+x /usr/local/bin/s3_upload
