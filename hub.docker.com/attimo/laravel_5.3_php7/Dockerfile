FROM ubuntu:16.04

RUN apt-get update && apt-get install -y php apache2 php-mysql php-zip php-mbstring php-xml libapache2-mod-php php-mcrypt curl python software-properties-common build-essential pkg-config libcairo2-dev libjpeg-dev libgif-dev libnotify-bin unzip zip sudo git vim 
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8 
RUN curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require "laravel/installer"
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
RUN sudo apt-get install -y nodejs
RUN curl -L https://npmjs.org/install.sh | sh
RUN npm install -g gulp
RUN echo export PATH="/root/.composer/vendor/bin:$PATH" >> /root/.bashrc
RUN /bin/bash -c "source /root/.bashrc"
RUN chmod -R 777 /var/www/html
COPY vhost.conf /etc/apache2/sites-available
RUN a2ensite vhost.conf
RUN a2enmod rewrite
RUN service apache2 start
