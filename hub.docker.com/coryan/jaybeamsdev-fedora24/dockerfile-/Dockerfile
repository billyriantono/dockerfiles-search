ARG PHPVERSION=7.4

FROM ubuntu:19.04

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

RUN apt-get update && apt-get upgrade -y && apt-get install -y \
  apt-utils \
  curl \
  wget \
  unzip \
  git \
  mysql-client \
  sudo \
  vim \
  bzip2 \
  htop \
  software-properties-common \
  build-essential \
  libssl-dev \
  libsqlite3-dev \
  ruby \
  ruby-dev

RUN add-apt-repository ppa:ondrej/php \
  && add-apt-repository ppa:ondrej/apache2 
  
RUN apt-get update \
  && apt-get install -y php$PHPVERSION \
  php$PHPVERSION-common \
  php$PHPVERSION-cli \
  php-apcu \
  php$PHPVERSION-curl \
  php$PHPVERSION-dev \
  php$PHPVERSION-mysql \
  php$PHPVERSION-curl \
  php$PHPVERSION-soap \
  php$PHPVERSION-intl \
  php$PHPVERSION-gd \
  php$PHPVERSION-mbstring \
  php$PHPVERSION-zip \
  php$PHPVERSION-xml \
  php$PHPVERSION-bcmath \
  php-xdebug \
  php-pear \
  php-memcache \
  libapache2-mod-php$PHPVERSION

# install the utils extensions we need
## COMPOSER ##
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
	&& php composer-setup.php \
	&& php -r "unlink('composer-setup.php');" \
	&& chmod +x composer.phar \
	&& mv composer.phar /usr/local/bin/composer
## DRUSH ##
#### REmoved by http://docs.drush.org/en/master/install/
## WP CLI ##
RUN wget  https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
	&& chmod +x wp-cli.phar \
	&& mv wp-cli.phar /usr/local/bin/wp
## NODE with NVM, GRUNT, BOWER ##
# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

ENV NVM_DIR /usr/local/nvm
#RUN curl https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | PROFILE=/etc/bash.bashrc /bin/bash \
#&& source $NVM_DIR/nvm.sh \
#
RUN mkdir -p $NVM_DIR \
        && wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash \
	&& source $NVM_DIR/nvm.sh \
        && nvm install 11 \
	&& nvm install 8 \
    	&& nvm install 6 \
	&& nvm install 4 \
    	&& nvm alias default 11 \
    	&& nvm use default \
	&& npm install npm -g \
	&& npm install -g grunt-cli bower http-server
## YARN ##
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg \
	&& apt-key add -echo "deb https://dl.yarnpkg.com/debian/ stable main" \
	&& tee /etc/apt/sources.list.d/yarn.list \
	&& apt-get update && apt-get install -y yarn

## SOME HACK on PHP ##
RUN rm -f /etc/php/7.3/apache2/conf.d/10-opcache.ini \
	&& rm -f /etc/php/7.3/apache2/conf.d/20-xdebug.ini \
	&& echo "export PHP_INI_SCAN_DIR=/etc/php/7.3/cli/conf.d:/etc/php/7.3/cli/conf.d/overrides" >> ~/.bashrc \
	&& a2enmod rewrite && a2enmod proxy && a2enmod proxy_http

RUN gem install mailcatcher && mailcatcher

ADD conf/10-sameuser-nopass /etc/sudoers.d/
ADD conf/user.sh / 
RUN /user.sh
COPY conf/httpd-foreground /usr/local/bin/

EXPOSE 80
EXPOSE 1025
EXPOSE 1080

WORKDIR /var/www/html

CMD ["httpd-foreground"]
