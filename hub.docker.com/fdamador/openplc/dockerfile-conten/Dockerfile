FROM ubuntu
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y --no-install-recommends php5 php5-mysql php5-gd imagemagick unzip curl build-essential
RUN apt-get install -y --no-install-recommends php5-cli
RUN curl -ksS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
RUN a2enmod rewrite
EXPOSE 80
CMD apachectl -DFOREGROUND
WORKDIR /var/www
