FROM ubuntu:disco

MAINTAINER "Taha PAKSU <tpaksu@gmail.com>"

RUN apt update -y \
    && apt-get install software-properties-common -y \
    && add-apt-repository ppa:ondrej/php -y \
    && apt update -y \
    && apt-get install -y tzdata \
    && apt-get install -y php7.2-fpm nginx php7.2-cli php7.2-curl php7.2-sqlite3 php7.2-mysql php7.2-curl \
        php7.2-json php7.2-cgi php7.2-xsl php7.0-mongo php7.2-mbstring composer curl nano

RUN mkdir /home/app/

ADD --chown=www-data:www-data . /home/app/

WORKDIR /home/app

RUN composer global require hirak/prestissimo
RUN composer install

ADD ./.docker/nginx.conf /etc/nginx/nginx.conf
ADD ./.docker/default.conf /etc/nginx/sites-enabled/default
ADD ./.docker/www.conf /etc/php/7.2/fpm/pool.d/www.conf
ADD ./.docker/start.sh /
RUN chmod +x /start.sh

EXPOSE 80

ENTRYPOINT ["/start.sh"]