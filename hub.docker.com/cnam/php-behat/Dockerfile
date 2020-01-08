FROM php:cli

RUN curl -sS https://getcomposer.org/installer | php \
&& mv composer.phar /usr/local/bin/composer

RUN apt update \
&& apt install -y zip \
&& apt install -y git \
&& apt install -y libapache2-mod-php5

COPY composer.json /composer.json

RUN composer update \
&& rm /usr/local/bin/composer \
&& ln /vendor/bin/behat /usr/local/bin/behat

CMD "/vendor/bin/behat init && /vendor/bin/behat"

