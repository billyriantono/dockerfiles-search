FROM diogodias2/bionic_essentials

USER root

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Lisbon


RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && add-apt-repository ppa:ondrej/php -y && apt-get update && apt-get install -y \
    apache2 \
    php-fpm  \
    php-curl \
    php-gd \
    php-intl \ 
    php-pear \
    php-imap \
    php-pspell \
    php-recode \
    php-tidy \
    php-xml \
    php-xmlrpc \
    zip \
    unzip \
    php7.2-zip \
    php7.2-mysql \
    mariadb-client \
    php-zip \
    php-mbstring \
    php-bcmath \ 
    php-soap \
    && wget https://getcomposer.org/installer -P /tmp/ \
    && cd /tmp && php installer && mv composer.phar /usr/local/bin/composer \
    && sudo mkdir -p /var/www/site && sudo chown -R www-data:www-data /var/www/site \
    && sudo chmod -R u=rwx,g=rwx,o=r /var/www/site \
    && sudo usermod -a -G www-data ubuntu \
    && sudo mkdir -p /home/ubuntu/./composer && sudo chown -R ubuntu /home/ubuntu/./composer 
    #&& echo 'export PATH="$HOME/.config/composer/vendor/bin:$PATH"' >> ~/.bashrc \
    #&& source ~/.bashrc


USER ubuntu

VOLUME /var/www/site

WORKDIR /var/www/site

CMD /bin/bash