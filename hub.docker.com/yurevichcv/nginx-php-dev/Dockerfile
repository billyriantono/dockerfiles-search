FROM maxexcloo/nginx-php:latest

MAINTAINER Constantine Yurevich

# Remove root directive from /etc/nginx/host.d/default.conf
RUN sed -i '/root/d' /etc/nginx/host.d/default.conf

# Remove unnecessary config file
RUN rm /etc/nginx/conf.d/02cache.conf

# Install PHP extensions
RUN apt-get update 
RUN apt-get install -y php5-dev
RUN apt-get install -y php-pear
RUN apt-get install -y libpcre3-dev
RUN apt-get install -y php5-apcu
ADD apcu.ini /etc/php5/mods-available/apcu.ini

# Install Xdebug
RUN apt-get update && apt-get install -y php5-xdebug
ADD xdebug.ini /etc/php5/mods-available/xdebug.ini

# Install SSH access (required for PHPStorm)
RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:root' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
# Change default login dir
RUN echo 'cd /data/http' >> "/root/.bashrc"
EXPOSE 22

# Intall MySQL client
RUN apt-get install -y mysql-client

# Install NodeJS & Grunt
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup | bash -
RUN apt-get install -y nodejs
RUN npm install -g grunt-cli

# Install Git
RUN apt-get install -y git

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

ADD config /config
ADD supervisord.conf /etc/supervisor/conf.d/sshd.conf

RUN mkdir /data/http
WORKDIR /data/http

ENV HOME /root

VOLUME /data
VOLUME /root/.ssh