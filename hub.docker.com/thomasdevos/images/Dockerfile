FROM ubuntu:xenial

RUN apt-get -y update

RUN apt-get install -y software-properties-common python-software-properties
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
RUN apt-get -y update

RUN apt-get install -y apache2 php7.2 libapache2-mod-php php7.2-mysql git zip mysql-client php7.2-curl php7.2-gd php7.2-mbstring software-properties-common python-software-properties vim --allow-unauthenticated curl apt-transport-https
RUN apt-get install -y php7.2-xml php7.2-intl

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get -y update
RUN apt-get install yarn -y

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

RUN addgroup thomas
RUN adduser --system --uid=1000 thomas
RUN usermod -a -G thomas thomas
RUN sed -i "s/www-data/thomas/" /etc/apache2/envvars

RUN a2enmod rewrite

WORKDIR /var/www/html/

CMD ["/usr/sbin/apache2ctl","-DFOREGROUND"]
