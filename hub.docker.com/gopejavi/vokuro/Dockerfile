FROM debian

RUN	apt-get update && \
	echo "mysql-server mysql-server/root_password root" | debconf-set-selections && \
	echo "mysql-server mysql-server/root_password_again root" | debconf-set-selections && \
	apt install -y mysql-server apache2 php php-mysql libapache2-mod-php composer git zip nano

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
RUN /usr/sbin/a2enmod rewrite
ADD 000-phalcon.conf /etc/apache2/sites-available/
RUN /usr/sbin/a2dissite '*' && /usr/sbin/a2ensite 000-phalcon

#RUN service mysql restart

WORKDIR /tmp

RUN	apt-get -y install php-dev libpcre3-dev gcc make && \
	git clone https://github.com/phalcon/cphalcon.git && \
	cd cphalcon/build/ && \
	./install && \
	cd /tmp && \
	/bin/rm -rf /tmp/cphalcon/ && \
	/usr/bin/apt-get -y purge php-dev libpcre3-dev gcc make && apt-get -y autoremove && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN	/bin/echo 'extension=phalcon.so' >/etc/php/7.0/mods-available/phalcon.ini

RUN	/usr/sbin/phpenmod phalcon


WORKDIR /var/www

RUN git clone https://github.com/gopejavi/vokuro.git && chmod -R 777 vokuro


WORKDIR /var/www/vokuro

RUN	service mysql restart && \
	echo "UPDATE user SET plugin='mysql_native_password',host='%' WHERE User='root'; FLUSH PRIVILEGES" | mysql -u root mysql && \
	echo "CREATE DATABASE vokuro CHARSET=utf8 COLLATE=utf8_unicode_ci" | mysql -u root && \
	sed -i "/bind-address/ s/^/# /" /etc/mysql/mariadb.conf.d/50-server.cnf
	

RUN	composer install

EXPOSE	80 3306

CMD	git pull origin master && \
	service mysql restart && \
	cat schemas/vokuro.sql | mysql -u root vokuro && \
	apache2ctl -D FOREGROUND
