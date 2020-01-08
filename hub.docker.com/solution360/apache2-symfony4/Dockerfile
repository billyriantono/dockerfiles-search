FROM debian:8

RUN apt-get update
RUN apt-get install -y wget curl apt-transport-https apache2 unzip
RUN apt-get install -y lsb-release ca-certificates
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg

# add dotdeb to apt sources list
RUN echo 'deb http://packages.dotdeb.org jessie all' > /etc/apt/sources.list.d/dotdeb.list
# Add PHP 7.1
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

## add dotdeb key for apt
RUN curl http://www.dotdeb.org/dotdeb.gpg | apt-key add -

RUN apt-get update

RUN apt-get install -y php7.1 php7.1-curl php7.1-gd php7.1-mbstring php7.1-imagick php7.1-mysql php7.1-xdebug php7.1-simplexml php7.1-zip php7.1-cli php7.1-common php7.1-json php7.1-opcache php7.1-xml php7.1-readline php7.1-sqlite3

#configure apache
RUN ["bin/bash", "-c", "sed -i 's/AllowOverride None/AllowOverride All\\nSetEnvIf X-Forwarded-Proto https HTTPS=on/g' /etc/apache2/apache2.conf"]

# Symfony4 needs a deeper positioned html root directory, such that the actual root is in /var/www/html/public but we still need to map the whole project into /var/www/html
RUN ["bin/bash", "-c", "mkdir /var/www/html/public"]
RUN ["bin/bash", "-c", "chown -R www-data:www-data /var/www/html/public"]
RUN ["bin/bash", "-c", "sed -i 's/DocumentRoot \\/var\\/www\\/html/DocumentRoot \\/var\\/www\\/html\\/public/g' /etc/apache2/sites-available/000-default.conf"]
RUN ["bin/bash", "-c", "sed -i 's/DocumentRoot \\/var\\/www\\/html/DocumentRoot \\/var\\/www\\/html\\/public/g' /etc/apache2/sites-available/default-ssl.conf"]

RUN service apache2 restart

#configure php
RUN ["bin/bash", "-c", "sed -i 's/max_execution_time\\s*=.*/max_execution_time=180/g' /etc/php/7*/apache2/php.ini"]
RUN ["bin/bash", "-c", "sed -i 's/upload_max_filesize\\s*=.*/upload_max_filesize=16M/g' /etc/php/7*/apache2/php.ini"]
RUN ["bin/bash", "-c", "sed -i 's/memory_limit\\s*=.*/memory_limit=256M/g' /etc/php/7*/apache2/php.ini"]
RUN ["bin/bash", "-c", "sed -i 's/post_max_size\\s*=.*/post_max_size=10M/g' /etc/php/7*/apache2/php.ini"]

#configure XDebug
RUN ["bin/bash", "-c", "echo [XDebug] >> /etc/php/7*/apache2/php.ini"]
RUN ["bin/bash", "-c", "echo xdebug.remote_enable=1 >> /etc/php/7*/apache2/php.ini"]
RUN ["bin/bash", "-c", "echo xdebug.remote_connect_back=1 >> /etc/php/7*/apache2/php.ini"]
RUN ["bin/bash", "-c", "echo xdebug.idekey=netbeans-xdebug >> /etc/php/7*/apache2/php.ini"]

# Configure apache
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2enmod proxy
RUN a2enmod headers
# enable ssl on apache
RUN a2ensite default-ssl
RUN chown -R www-data:www-data /var/www
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
RUN service apache2 restart

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
