FROM ubuntu:latest

RUN mkdir /var/www/
RUN mkdir /var/www/html
COPY codice/ /var/www/html

################# SET PERMESSI ###################################

RUN useradd magento
RUN usermod -g www-data magento
RUN cd /var/www/html/magento && find var vendor pub/static pub/media app/etc -type f -exec chmod g+w {} \;

RUN cd /var/www/html/magento && find var vendor pub/static pub/media app/etc -type d -exec chmod g+ws {} \;
RUN cd /var/www/html/magento && chown -R magento:www-data .
RUN cd /var/www/html/magento && chmod u+x bin/magento


RUN apt-get update && apt-get install -y nano
################ FINE # SET PERMESSI ##############################

#INSTALLARE GIT
#RUN apt-get update && apt-get install -y git

# install dependencies
RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		apache2 \
		ca-certificates openssl \
		curl \
		php7.0 \
		php7.0-curl \
		php7.0-gd \
		php7.0-json \
		php7.0-simplexml \
		php7.0-mbstring \
		php-bcmath \
		php7.0-mysql \
		php7.0-zip \
                php-soap \
		openssh-server \
		composer \
		php7.0-mcrypt \
		php7.0-intl \
                supervisor  \
		libapache2-mod-php7.0 \
	&& rm -r /var/lib/apt/lists/*
RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf
RUN a2enmod rewrite expires
RUN a2enmod ssl
RUN a2enmod headers

RUN mkdir /var/run/sshd
RUN echo 'root:screencast' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN  sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/g' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

RUN apt-get update 

# installazione grunt
RUN curl -sL https://deb.nodesource.com/setup_8.x
RUN apt-get install -y nodejs
RUN apt-get install -y npm
#RUN npm install -g grunt-cli
  



# commentato composer install, poi chiamarlo da dentro al conteiner
#  RUN cd /var/www/html && composer install

RUN service apache2 restart
#RUN chmod -R 777 /var/www/html/app/ var/www/html/var/ var/www/html/pub
RUN chmod -R 777 /var/www/html

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

################# XDEBUG ###################################

  #pacchetti che servono per installare pecl xdebug (solo per magento)
  RUN apt-get update 
  RUN apt-get install -y php-pear
  RUN apt-get install -y php-dev
  
  #setting xdebug
  RUN yes | pecl install xdebug \
      && echo "zend_extension=$(find /usr/lib/php/20151012/ -name xdebug.so)" > /usr/local/etc/xdebug.ini \
      && echo "xdebug.default_enable=1" >> /usr/local/etc/xdebug.ini \
      && echo "xdebug.remote_autostart=1" >> /usr/local/etc/xdebug.ini \
      && echo "xdebug.remote_connect_back=1" >> /usr/local/etc/xdebug.ini \
      && echo "xdebug.remote_enable=1" >> /usr/local/etc/xdebug.ini \
      && echo "xdebug.remote_port=9000" >> /usr/local/etc/xdebug.ini \
      && echo "xdebug.idekey=netbeans-xdebug" >> /usr/local/etc/xdebug.ini \
      && echo "xdebug.remote_handler=dbgp" >> /usr/local/etc/xdebug.ini
      
  #istruzioni inserite per far funzionare il debug per la versione EE di Magento 2.2
      RUN echo "zend_extension=$(find /usr/lib/php/20151012/ -name xdebug.so)" >> /etc/php/7.0/apache2/php.ini \
      && echo "xdebug.default_enable=1" >> /etc/php/7.0/apache2/php.ini \
      && echo "xdebug.remote_autostart=1" >> /etc/php/7.0/apache2/php.ini \
      && echo "xdebug.remote_connect_back=1" >> /etc/php/7.0/apache2/php.ini \
      && echo "xdebug.remote_enable=1" >> /etc/php/7.0/apache2/php.ini \
      && echo "xdebug.remote_port=9000" >> /etc/php/7.0/apache2/php.ini \
      && echo "xdebug.idekey=netbeans-xdebug" >> /etc/php/7.0/apache2/php.ini \
      && echo "xdebug.remote_handler=dbgp" >> /etc/php/7.0/apache2/php.ini

################ FINE # XDEBUG ###############################

RUN cd var/www/


## Mount ##
WORKDIR /var/www/html
#VOLUME /var/www/html

# Default command	
#CMD ["apachectl", "-D", "FOREGROUND"] 
# Ports
EXPOSE 80
EXPOSE 443
EXPOSE 22
CMD ["/usr/bin/supervisord"]




