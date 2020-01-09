FROM circleci/php:7.2.6-zts-node-browsers

RUN sudo apt-get install -y curl libpng-dev libxml2-dev zlib1g-dev libicu-dev g++ libmcrypt-dev libreadline-dev libxml2 libxml2-dev libxslt1-dev libfreetype6-dev libicu-dev libjpeg62-turbo-dev libmcrypt-dev libpng-dev libxslt1-dev sendmail-bin sendmail cron rsyslog git libgd-dev mysql-client
RUN sudo docker-php-ext-configure intl
RUN sudo docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr --with-png-dir=/usr
RUN sudo docker-php-ext-install pdo_mysql gd intl bcmath soap xsl mbstring json xml mysqli sockets zip
RUN sudo apt install -y mysql-client
RUN sudo touch /usr/local/etc/php/conf.d/memory_limit.ini
RUN echo "memory_limit = 768M" | sudo tee -a /usr/local/etc/php/conf.d/memory_limit.ini
