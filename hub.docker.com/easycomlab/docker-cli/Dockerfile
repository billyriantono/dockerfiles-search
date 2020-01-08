FROM php:7.1-cli
MAINTAINER EasycomLab <easycomlab@easycom.digital>

# =========================================
# RUN update
# =========================================
RUN apt-get update

# =========================================
# Install dependencies
# =========================================
RUN apt-get install -y \
    libfreetype6-dev \
    openssh-server \
    imagemagick \
    graphicsmagick \
    curl \
    ca-certificates \
    gzip \
    zip \
    less \
    bzip2 \
    wget \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxslt1-dev \
    sudo \
    cron \
    rsyslog \
    mysql-client \
    libmagickwand-dev \
    libmagickcore-dev \
    apt-transport-https

# =========================================
# Install tools
# =========================================
RUN apt-get install -y \
    nano \
    vim \
    htop \
    iptraf \
    ssmtp \
    openssl \
    git \
    gnupg
    
# =========================================
# Install yarn
# =========================================    
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn

# =========================================
# Install npm
# =========================================
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

# =========================================
# Install npm tools
# =========================================
RUN npm install -g less
RUN npm install -g bower
RUN npm install -g gulp-cli

# =========================================
# Configure the GD library
# =========================================
RUN docker-php-ext-configure \
gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

# =========================================
# Install php required extensions
# =========================================
RUN docker-php-ext-install \
  dom \
  gd \
  intl \
  mbstring \
  pdo_mysql \
  xsl \
  zip \
  soap \
  mcrypt \
  mysqli \
  bcmath \
  exif
  
# =========================================
# Install apcu
# =========================================
RUN pecl install -f apcu

# =========================================
# Install imagick
# =========================================
RUN pecl install -f imagick  

# =========================================
# Set ENV variables
# =========================================
ENV DEBUG false
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV PROJECT_ROOT /var/www/htdocs

# Get composer installed to /usr/local/bin/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# =========================================
# Configure SSHD
# =========================================
RUN sed -ri 's,^PermitRootLogin\s+.*,PermitRootLogin no,' /etc/ssh/sshd_config \
	&& sed -ri 's,UsePAM yes,#UsePAM yes,g' /etc/ssh/sshd_config \
	&& sed -ri 's,#PasswordAuthentication yes,PasswordAuthentication no,g' /etc/ssh/sshd_config \
	&& sed -ri 's,^X11Forwarding\s+.*,X11Forwarding no,' /etc/ssh/sshd_config \
	&& sed -ri 's,^HostKey /etc/ssh/ssh_host_,HostKey /etc/ssh/keys/ssh_host_,' /etc/ssh/sshd_config \
	&& mkdir /var/run/sshd \
&& service ssh stop

# =========================================
# Create easycom user
# =========================================
RUN openssl rand -base64 32 > ./.pass \
	&& useradd -ms /bin/bash --password='$(cat ./.pass)' easycom \
	&& adduser easycom ssh \
	&& echo "$(cat ./.pass)\n$(cat ./.pass)\n" | passwd easycom \
	&& mv ./.pass /home/easycom/ \
	&& chown -Rf easycom:easycom /home/easycom

#Add custom bashrc
ADD ./bashrc.easycom /home/easycom/.bashrc

# =========================================
# Our capistrano script will create a local git after deploy to allow remote check of unallowed local changes ; so git must be configured
# =========================================
USER easycom
RUN git config --global user.email "easycom-$(cat /etc/hostname)@easycom.digital" \
	&& git config --global user.name "User Easycom - Docker Capistrano $(cat /etc/hostname)"

# =========================================
# SETUP SCRIPTS
# =========================================
USER root
ADD bin/* /usr/local/bin/
# MAGENTO2
RUN ["chmod", "+x", "/usr/local/bin/magento-installer"]
RUN ["chmod", "+x", "/usr/local/bin/magento-command"]
RUN ["chmod", "+x", "/usr/local/bin/wp-installer"]
RUN ["chmod", "+x", "/usr/local/bin/run-cron"]

ADD etc/php-fpm.ini /usr/local/etc/php/conf.d/zz-custom.ini

# =========================================
# Set entrypoint
# =========================================
ADD docker-entrypoint.sh /docker-entrypoint.sh
RUN ["chmod", "+x", "/docker-entrypoint.sh"]
ENTRYPOINT ["/docker-entrypoint.sh"]

VOLUME /root/.composer/cache
VOLUME /home/easycom/.composer/cache

WORKDIR $PROJECT_ROOT

EXPOSE 22

# Launch run script
CMD ["-D"]
