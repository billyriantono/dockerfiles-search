FROM php:7.0.11-apache
RUN useradd -u 1000 -m www-bridge-user

RUN apt-get update && curl -sL https://deb.nodesource.com/setup_4.x | bash -
RUN apt-get install -m -y \
	git \
	wget \
	zlib1g-dev \
	zip \
	vim \
	mysql-client \
	libpng12-dev \
	libmcrypt-dev \
	libicu-dev \
	nodejs \
	libfreetype6-dev \
	libjpeg62-turbo-dev \
	ssmtp \
	atool \
	nano \
	curl \
	wget \
	sudo \
	openssh-server \
	locate \
	libxml2-dev \
	&& docker-php-ext-install mbstring \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install gd \
	&& docker-php-ext-install mcrypt \
	&& docker-php-ext-install iconv \
	&& docker-php-ext-install opcache \
	&& docker-php-ext-install pcntl \
	&& docker-php-ext-install intl \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install soap \
	&& docker-php-ext-install bcmath \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& curl -sS https://getcomposer.org/installer | php \
	&& mv composer.phar /usr/bin/composer \
	&& pecl install xdebug \
	&& a2enmod rewrite

ADD apache/templates/apache2.conf /etc/apache2/
ADD apache/templates/vhost.conf /etc/apache2/sites-available/
ADD apache/templates/php.ini /usr/local/etc/php/
ADD apache/templates/ssmtp.conf /etc/ssmtp/
ADD apache/templates/xdebug.ini /usr/local/etc/php/conf.d/
RUN a2ensite vhost.conf

# Copy apache scripts 
RUN mkdir /opt/apache-scripts
COPY apache/scripts /opt/apache-scripts
ENV PATH /opt/apache-scripts:$PATH

# Setup SSH.
RUN echo 'root:root' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN mkdir /var/run/sshd && chmod 0755 /var/run/sshd
RUN mkdir -p /root/.ssh/
ADD utils/ssh/authorized_keys /root/.ssh/authorized_keys
ADD utils/ssh/id_rsa /root/.ssh/id_rsa
ADD utils/ssh/id_rsa.pub /root/.ssh/id_rsa.pub
ADD utils/ssh/known_hosts /root/.ssh/known_hosts
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

# Install Drush 8.
RUN php -r "readfile('http://files.drush.org/drush.phar');" > /usr/local/bin/drush
RUN chmod +x /usr/local/bin/drush

# Install Drupal Console.
#RUN curl http://drupalconsole.com/installer -L -o drupal.phar
#RUN mv drupal.phar /usr/local/bin/drupal && chmod +x /usr/local/bin/drupal
#RUN drupal init

# Compass + Sass
#RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
# RVM + Ruby 
#RUN \curl -sSL https://get.rvm.io | bash -s stable --ruby
# @TODO this should be in the bash profile
#RUN source /usr/local/rvm/scripts/rvm

# Install Gem
#RUN npm update -g npm
#RUN npm install -g gem

# Install compass
#RUN gem update --system && gem install compass

# Install bower
#RUN npm install -g bower

# Install bundler
#RUN npm install -g bundler
#RUN npm install bundler

# Install Grunt
#RUN npm install -g grunt-cli

# Install Gulp
#RUN npm install -g gulp-cli

# Update files db
RUN updatedb

# Normal workdir
WORKDIR /var/www
