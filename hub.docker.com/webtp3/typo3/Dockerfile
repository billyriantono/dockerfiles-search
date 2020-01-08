FROM ubuntu:xenial
MAINTAINER Thomas Ruta <email@thomasruta.de>

#prepair Server
#RUN sudo -s
#RUN sudo passwd root
RUN apt-get update && \
    apt-get -yq install ssh openssh-server vim-nox software-properties-common python-software-properties mysql-client git curl bash   && \
    LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php
# Install packages
RUN apt-get update && \
    apt-get -yq --force-yes install  apache2 apache2-doc apache2-utils libapache2-mod-fcgid apache2-suexec-pristine php-pear mcrypt \
    libapache2-mod-php  php7.0 php7.0-common php7.0-gd php7.0-mysql php7.0-imap php7.0-cli php7.0-cgi libapache2-mod-fcgid apache2-suexec-pristine \
    php-pear php-auth php7.0-mcrypt mcrypt  imagemagick libruby libapache2-mod-python php7.0-curl php7.0-intl php7.0-pspell php7.0-recode php7.0-sqlite3 php7.0-tidy \
    php7.0-xmlrpc php7.0-xsl php7.0-zip php7.0-mbstring  php7.0-soap  php7.0-json php7.0-opcache libapache2-mod-fastcgi php7.0-fpm php7.0-apcu


RUN apt-get update && \
    apt-get -yq --force-yes install   \
    libapache2-mod-php  php7.1 php7.1-common php7.1-gd php7.1-mysql php7.1-imap php7.1-cli php7.1-cgi  \
    php-pear php-auth php7.1-mcrypt mcrypt  imagemagick libruby libapache2-mod-python php7.1-apcu php7.1-curl php7.1-intl php7.1-pspell php7.1-recode php7.1-sqlite3 php7.1-tidy \
    php7.1-xmlrpc php7.1-xsl php7.1-zip php7.1-mbstring  php7.1-soap  php7.1-json php7.1-opcache php7.1-fpm \
    memcached php-memcache php-imagick php-gettext  php-apcu  php-xdebug  phpunit phpunit-dbunit  phpunit-mock-object graphicsmagick imagemagick poppler-utils default-jre

# Manually set up the apache environment variables

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid


# config apache
RUN a2enmod rewrite ssl actions include cgi
RUN a2enmod dav_fs dav auth_digest headers
RUN a2enmod fastcgi alias


#RUN apt-get install php7.0-opcache php-apcu libapache2-mod-fastcgi php7.0-fpm
RUN rm /etc/apache2/sites-enabled/000-default.conf -rf
RUN mkdir /var/www/php-fcgi-scripts && mkdir /var/www/tmp && mkdir /var/www/cgi-bin  /var/www/html/web

RUN useradd -m -g www-data -s /bin/bash typo3user
ADD .php-fcgi-starter /var/www/php-fcgi-scripts/
RUN echo AllowUsers typo3user >> /etc/ssh/sshd_config && sed -i "s/.*PasswordAuthentication .*/PasswordAuthentication  yes/g" /etc/ssh/sshd_config

RUN chmod 775 /var/www/php-fcgi-scripts/.php-fcgi-starter && chown www-data:www-data /var/www/php-fcgi-scripts/.php-fcgi-starter && \
    chmod 775 /var/www/tmp && chown www-data:www-data /var/www/tmp


# Adjust some php settings
ADD typo3.php.ini /etc/php/7.0/cgi/conf.d/
ADD typo3.php.ini /etc/php/7.1/cgi/conf.d/
ADD typo3.php.ini /etc/php/7.2/cgi/conf.d/

#change php to 7.1
RUN rm /etc/alternatives/php && ln -s /usr/bin/php7.1 /etc/alternatives/php
RUN rm /etc/alternatives/php-cgi && ln -s /usr/bin/php-cgi7.1 /etc/alternatives/php-cgi

# place run script
ADD run-typo3.sh /var/www/cgi-bin/
RUN chmod 755 /var/www/cgi-bin/

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
RUN php composer-setup.php --install-dir=/usr/local/bin --filename=composer
RUN php -r "unlink('composer-setup.php');"



# Expose environment variables
ENV PHP_VERSION 7.1
ENV DB_HOST db
ENV DB_PORT 3306
ENV ADMIN_USER tp3min
ENV ADMIN_PASS Init1111
ENV DB_NAME typo3
ENV DB_USER root
ENV DB_PASS my-secret-pw
ENV INSTALL_TOOL_PASSWORD password

RUN service ssh restart

#install typo3
#RUN bash /var/www/cgi-bin/run-typo3.sh

EXPOSE 80
#ssh
EXPOSE 22
#Xdebug
EXPOSE 9000
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]


