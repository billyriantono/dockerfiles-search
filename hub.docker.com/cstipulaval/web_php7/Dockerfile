FROM ubuntu:16.04

RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install php7.0 php7.0-cli php7.0-mysql php7.0-ldap php7.0-intl php7.0-curl apache2 libapache2-mod-php7.0 curl php7.0-zip php-xml mysql-client php-mbstring php7.0-mbstring php7.0-gd php7.0-soap subversion zip unzip php7.0-mcrypt nano vim git dos2unix iputils-ping php7.0-imap

# paquets pour installer wkhtml
RUN apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install wget fontconfig xfonts-75dpi xfonts-base

# paquets pour utiliser wkhtml
RUN apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install libxrender1 libxext6 libfontconfig1
 
# paquets pour installer oci8
RUN apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install alien build-essential php7.0-dev php-pear 

# paquets pour utiliser oci8
RUN apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install libaio1 

# paquets pour installer mailhog
RUN apt-get update && apt-get install --no-install-recommends --assume-yes --quiet ca-certificates git && rm -rf /var/lib/apt/lists/*

# installer mailhog
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' >> /etc/php/7.0/apache2/php.ini
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' >> /etc/php/7.0/cli/php.ini

# Enable apache mods.
RUN a2enmod php7.0
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2ensite default-ssl

# Update the PHP.ini file, enable <? ?> tags and quieten logging.
RUN sed -i "s/error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT/error_reporting = E_ALL \& ~E_NOTICE \& ~E_DEPRECATED/" /etc/php/7.0/apache2/php.ini

# définir le fuseau horaire sur le serveur et dans PHP
# pour définir la date dans Ubuntu 16.04
RUN ln -fs /usr/share/zoneinfo/Canada/Eastern /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata

RUN sed -i "s/;date.timezone.*/date.timezone ='America\/Toronto'/" /etc/php/7.0/apache2/php.ini

# augmenter la limite de la mémoire pour php à 1024M.
RUN sed -i "s/memory_limit.*/memory_limit = 1024M/" /etc/php/7.0/apache2/php.ini

# augmenter la taille du paramètre POST_MAX_SIZE
RUN sed -i "s/post_max_size.*/post_max_size = 1000M/" /etc/php/7.0/apache2/php.ini

# augmenter la taille du paramètre UPLOAD_MAX_FILESIZE
RUN sed -i "s/upload_max_filesize.*/upload_max_filesize = 1000M/" /etc/php/7.0/apache2/php.ini

# Pour la configuration du client LDAP.
RUN sed -i -e "\$aTLS_REQCERT never" /etc/ldap/ldap.conf

# Ajouter l'utilisateur cstip
RUN useradd -ms /bin/bash cstip

# rouler apache en tant que cstip
RUN sed -i -e "\$aUser cstip" /etc/apache2/apache2.conf
RUN sed -i -e "\$aGroup cstip" /etc/apache2/apache2.conf
# RUN sed -i -e "\$aGroup cstip" /etc/apache2/apache2.conf
# RUN sed -i -e "s/ErrorLog \${APACHE_LOG_DIR}/ErrorLog \/tmp\/log\/apache2/" /etc/apache2/apache2.conf
# RUN sed -i -e "s/ErrorLog \${APACHE_LOG_DIR}/ErrorLog \/tmp\/log\/apache2/" /etc/apache2/apache2.conf
# RUN sed -i -e "s/ErrorLog \${APACHE_LOG_DIR}/ErrorLog \/tmp\/log\/apache2/" /etc/apache2/apache2.conf

# Manually set up the apache environment variables
# ENV APACHE_RUN_USER cstip
# ENV APACHE_RUN_GROUP cstip
# ENV APACHE_LOG_DIR /var/log/apache2
# ENV APACHE_LOCK_DIR /var/lock/apache2
# ENV APACHE_PID_FILE /var/run/apache2.pid
# ENV APACHE_LOG_DIR /tmp/log/apache2
# ENV APACHE_LOCK_DIR /tmp/lock/apache2
# ENV APACHE_PID_FILE /tmp/run/apache2.pid


# le conteneur roulera sur le port 80 dans le conteneur
EXPOSE 80
EXPOSE 443

# Update the default apache site with the config we created.
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf
ADD apache-config-ssl.conf /etc/apache2/sites-available/default-ssl.conf

# le répertoire courant devient /var/www; toutes les commandes lancées à partir de docker exec seront executés à partir de ce répertoire
WORKDIR /var/www

# installer Composer
ADD installer_composer.sh .
RUN chmod a+x installer_composer.sh
RUN ./installer_composer.sh
RUN mv composer.phar /usr/local/bin/composer
RUN rm installer_composer.sh

# installer wkhtmlpdf
# RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
# RUN tar xf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
# RUN cp wkhtmltox/bin/wkhtmltopdf /usr/bin
# RUN rm wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb
RUN dpkg -i wkhtmltox_0.12.5-1.xenial_amd64.deb
# RUN apt-get install -f
# RUN rm -R wkhtmltox

# installer oci8
ADD oci8/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm /tmp/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
ADD oci8/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm /tmp/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm
RUN alien -i /tmp/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
RUN alien -i /tmp/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm
RUN pecl install oci8 # Source : https://pecl.php.net/package/oci8
RUN echo "extension=oci8.so" >> /etc/php/7.0/apache2/php.ini
RUN echo "extension=oci8.so" >> /etc/php/7.0/cli/php.ini
RUN rm /tmp/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
RUN rm /tmp/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm

#Pour Drupal console
RUN curl https://drupalconsole.com/installer -L -o drupal.phar
RUN mv drupal.phar /usr/local/bin/drupal
RUN chmod +x /usr/local/bin/drupal

# Installer Drush launcher
RUN wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/download/0.6.0/drush.phar
RUN chmod +x drush.phar
RUN mv drush.phar /usr/local/bin/drush

# Activer le module mcrypt de php
#RUN ln -s /etc/php5/mods-available/mcrypt.ini /etc/php5/apache2/conf.d/20-mcrypt.ini
#RUN ln -s /etc/php5/mods-available/mcrypt.ini /etc/php5/cli/conf.d/20-mcrypt.ini
#RUN ln -s /etc/php/7.0/mods-available/mcrypt.ini /etc/php/7.0/apache2/conf.d/20-mcrypt.ini
#RUN ln -s /etc/php/7.0/mods-available/mcrypt.ini /etc/php/7.0/cli/conf.d/20-mcrypt.ini

# Installer Xdebug
RUN pecl install xdebug
RUN echo "zend_extension='/usr/lib/php/20151012/xdebug.so'" >> /etc/php/7.0/apache2/php.ini
RUN echo "xdebug.remote_autostart = 1" >> /etc/php/7.0/apache2/php.ini
RUN echo "xdebug.remote_enable = 1" >> /etc/php/7.0/apache2/php.ini
RUN echo "xdebug.remote_log = /tmp/xdebug.log" >> /etc/php/7.0/apache2/php.ini
RUN echo "xdebug.remote_host = localhost" >> /etc/php/7.0/apache2/php.ini

# Installer PHPUnit
RUN wget https://phar.phpunit.de/phpunit-6.5.phar
RUN chmod +x phpunit-6.5.phar
RUN mv phpunit-6.5.phar /usr/local/bin/phpunit

# Installer NPM
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get install -y nodejs

# supprimer les paquets qui ne sont plus nécessaires
RUN apt-get -y autoremove alien build-essential php7.0-dev php-pear

# démarrer apache2
CMD /usr/sbin/apache2ctl -D FOREGROUND
