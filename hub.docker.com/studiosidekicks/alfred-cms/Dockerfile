FROM nanoninja/php-fpm:7.3.6
COPY --from=composer:1.9.0 /usr/bin/composer /usr/bin/composer

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get update && apt-get install -y nodejs

RUN mkdir /usr/src/app
WORKDIR /usr/src/app
RUN npm install -g grunt-cli