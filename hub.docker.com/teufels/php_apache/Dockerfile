#+++++++++++++++++++++++++++++++++++++++
# Dockerfile for teufels/php-apache
#+++++++++++++++++++++++++++++++++++++++

FROM php:7.1-apache-jessie

# enable mods
RUN a2enmod rewrite \
	&& a2enmod headers

COPY etc/             /opt/docker/etc/

# apt
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
	&& apt-get update \
	&& apt-get install -y xz-utils \
	&& apt-get install -y libxrender1 \
    && apt-get install -y \
    	apt-transport-https \ 
    	lsb-release \
    	libbz2-dev \
    	libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng12-dev \
		libpq-dev \
		libxml2-dev \
		libxslt1.1 libxslt1-dev \
		libc-client-dev libkrb5-dev \
    	ca-certificates \
    	wget \
    	nano \
    	mysql-client \
    	zsh \
    	git \
    	gdebi \
    	build-essential libssl-dev libxrender-dev \
    	nodejs \
    	sudo \
    	vim

# gulp
RUN npm install -g gulp \
	 && npm install --save-dev gulp \
	 && npm install -global less \
	 && npm install gulp-less \
	 && npm install -g node-sass \
	 && npm install gulp-sass --save-dev \
	 && npm install gulp-clean-css --save-dev \
	 && npm install --save-dev gulp-autoprefixer \
	 && npm install --save-dev gulp-wrap \
	 && npm install --save-dev gulp-tap \
	 && npm install --save-dev gulp-file-include \
	 && npm install gulp-concat gulp-rename gulp-uglify --save-dev \
	 && npm install --save-dev gulp-util \
	 && npm install --save-dev gulp-debug


# pecl
RUN pecl install xdebug \
	&& pecl install apcu \
	&& docker-php-ext-enable xdebug apcu

# docker-php-ext-install
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
	&& docker-php-ext-install imap \
	&& docker-php-ext-install opcache \
	&& docker-php-ext-install bcmath \
	&& docker-php-ext-install calendar \
	&& docker-php-ext-install bz2 \
	&& docker-php-ext-install ctype \
	&& docker-php-ext-install dba \
	&& docker-php-ext-install exif \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install gd \
	&& docker-php-ext-install gettext \
	&& docker-php-ext-install mcrypt \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install pgsql \
	&& docker-php-ext-install soap \
	&& docker-php-ext-install wddx \
	&& docker-php-ext-install xsl \
	&& docker-php-ext-install zip \
	&& docker-php-ext-enable opcache bcmath calendar bz2 ctype dba gd gettext exif imap mcrypt mysqli pdo_mysql pgsql soap wddx xsl zip

# ioncube loader
RUN curl -o ioncube.tar.gz http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
    && tar -xvvzf ioncube.tar.gz \
    && mv ioncube/ioncube_loader_lin_7.1.so `php-config --extension-dir` \
    && rm -Rf ioncube.tar.gz ioncube \
    && docker-php-ext-enable ioncube_loader_lin_7.1

# wkhtml
#RUN wget https://bitbucket.org/wkhtmltopdf/wkhtmltopdf/downloads/wkhtmltox-0.13.0-alpha-7b36694_linux-jessie-amd64.deb \
RUN gdebi --n /opt/docker/etc/wkhtmltox-0.13.0-alpha-7b36694_linux-jessie-amd64.deb

# oh-my-zsh
RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true \
	&& chsh -s /bin/zsh \
	&& chsh -s /bin/zsh www-data