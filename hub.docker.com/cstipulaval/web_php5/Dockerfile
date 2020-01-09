FROM ubuntu:14.04

RUN apt-get update && apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install php5 php5-cli php5-mysql php5-ldap php5-intl php5-curl apache2 libapache2-mod-php5 curl mysql-client php5-gd subversion zip unzip php5-mcrypt php-soap nano vim git

# paquets pour installer wkhtml
RUN apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install xz-utils wget 

# paquets pour utiliser wkhtml
RUN apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install libxrender1 libxext6 libfontconfig1
 
# paquets pour installer oci8
RUN apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install alien build-essential php5-dev php-pear 

# paquets pour utiliser oci8
RUN apt-get -y upgrade && DEBIAN_FRONTEND=noninteractive apt-get -y install libaio1 

# paquets pour installer mailhog
RUN apt-get update && apt-get install --no-install-recommends --assume-yes --quiet ca-certificates git && rm -rf /var/lib/apt/lists/*

# installer mailhog
RUN curl -Lsf 'https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz' | tar -C '/usr/local' -xvzf -
ENV PATH /usr/local/go/bin:$PATH
RUN go get github.com/mailhog/mhsendmail
RUN cp /root/go/bin/mhsendmail /usr/bin/mhsendmail
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' >> /etc/php5/apache2/php.ini
RUN echo 'sendmail_path = /usr/bin/mhsendmail --smtp-addr mailhog:1025' >> /etc/php5/cli/php.ini

# Enable apache mods.
RUN a2enmod php5
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2ensite default-ssl

# Update the PHP.ini file, enable <? ?> tags and quieten logging.
RUN sed -i "s/error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT/error_reporting = E_ALL \& ~E_NOTICE \& ~E_DEPRECATED/" /etc/php5/apache2/php.ini

# définir le fuseau horaire sur le serveur et dans PHP
# pour définir la date dans Ubuntu 14.04
RUN sudo echo "America/Toronto" > /etc/timezone
RUN sudo dpkg-reconfigure -f noninteractive tzdata
RUN sed -i "s/;date.timezone.*/date.timezone ='America\/Toronto'/" /etc/php5/apache2/php.ini

# augmenter la limite de la mémoire pour php à 1024M.
RUN sed -i "s/memory_limit.*/memory_limit = 1024M/" /etc/php5/apache2/php.ini

# augmenter la taille du paramètre POST_MAX_SIZE
RUN sed -i "s/post_max_size.*/post_max_size = 1000M/" /etc/php5/apache2/php.ini

# augmenter la taille du paramètre UPLOAD_MAX_FILESIZE
RUN sed -i "s/upload_max_filesize.*/upload_max_filesize = 1000M/" /etc/php5/apache2/php.ini

# Pour la configuration du client LDAP.
RUN sed -i -e "\$aTLS_REQCERT never" /etc/ldap/ldap.conf

# Ajouter l'utilisateur cstip
RUN useradd -ms /bin/bash cstip

# rouler apache en tant que cstip
RUN sed -i -e "\$aUser cstip" /etc/apache2/apache2.conf
RUN sed -i -e "\$aGroup cstip" /etc/apache2/apache2.conf

# Manually set up the apache environment variables
# ENV APACHE_RUN_USER www-data
# ENV APACHE_RUN_GROUP www-data
# ENV APACHE_LOG_DIR /var/log/apache2
# ENV APACHE_LOCK_DIR /var/lock/apache2
# ENV APACHE_PID_FILE /var/run/apache2.pid

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
RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
RUN tar xf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
RUN cp wkhtmltox/bin/wkhtmltopdf /usr/bin
RUN rm wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
RUN rm -R wkhtmltox

# installer oci8
ADD oci8/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm /tmp/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
ADD oci8/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm /tmp/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm
RUN alien -i /tmp/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
RUN alien -i /tmp/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm
RUN pecl install oci8-2.0.12 # Source : https://pecl.php.net/package/oci8
RUN echo "extension=oci8.so" >> /etc/php5/apache2/php.ini
RUN rm /tmp/oracle-instantclient12.1-basic-12.1.0.2.0-1.x86_64.rpm
RUN rm /tmp/oracle-instantclient12.1-devel-12.1.0.2.0-1.x86_64.rpm

#Pour Drupal console
RUN curl https://drupalconsole.com/installer -L -o drupal.phar
RUN mv drupal.phar /usr/local/bin/drupal
RUN chmod +x /usr/local/bin/drupal

# Installer Drush launcher
RUN wget -O drush.phar https://github.com/drush-ops/drush-launcher/releases/download/0.5.1/drush.phar
RUN chmod +x drush.phar
RUN mv drush.phar /usr/local/bin/drush

# Activer le module mcrypt de php
RUN ln -s /etc/php5/mods-available/mcrypt.ini /etc/php5/apache2/conf.d/20-mcrypt.ini
RUN ln -s /etc/php5/mods-available/mcrypt.ini /etc/php5/cli/conf.d/20-mcrypt.ini

# supprimer les paquets qui ne sont plus nécessaires
RUN apt-get -y autoremove alien build-essential php5-dev php-pear

# démarrer apache2
CMD /usr/sbin/apache2ctl -D FOREGROUND
