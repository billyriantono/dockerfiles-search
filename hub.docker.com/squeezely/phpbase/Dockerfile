FROM ubuntu:bionic
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install language-pack-en-base software-properties-common -y
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y php7.2-cli php7.2-curl php7.2-mysql php7.2-dev php7.2-mbstring php7.2-soap php7.2-xml php7.2-zip php7.2-intl php-msgpack php-memcached php-amqp php-imagick php-oauth
RUN pecl install redis && echo "extension=redis.so" > /etc/php/7.2/mods-available/redis.ini

RUN echo "deb http://apt.newrelic.com/debian/ newrelic non-free" | tee /etc/apt/sources.list.d/newrelic.list && \
curl -s https://download.newrelic.com/548C16BF.gpg | apt-key add - && \
apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y newrelic-php5

COPY newrelic.ini /etc/php/7.2/mods-available/newrelic.ini

COPY entrypoint.sh /usr/local/bin/
RUN ln -s usr/local/bin/entrypoint.sh / # backwards compat
ENTRYPOINT ["entrypoint.sh"]
