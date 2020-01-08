FROM oprax/debian:stable

LABEL maintainer="oprax@me.com"

RUN wget -qO - https://packages.sury.org/php/apt.gpg | apt-key add -
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list
RUN apt-get update
RUN apt-get install -y \
    php7.1-cli \
    php7.1-curl \
    php7.1-xdebug \
    php7.1-mysql \
    php7.1-sqlite \
    php7.1-mbstring \
    php7.1-gd \
    php7.1-xml \
    php7.1-zip \
    php7.1-bcmath \
    php7.1-intl

COPY composer-setup.sh /opt/composer-setup.sh

RUN chmod +x /opt/composer-setup.sh && /opt/composer-setup.sh

