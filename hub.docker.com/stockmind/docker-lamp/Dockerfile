FROM mattrayner/lamp:latest-1604

# Install memcached for Laravel/Lumen support
RUN apt-get update && \
	 apt-get -y install php-memcached memcached && \
	 rm -rf /var/lib/apt/lists/*
	 
RUN apt-get update && \
	 apt-get -y install php7.2 php7.2-common php7.2-mbstring php7.2-xml php7.2-ldap libapache2-mod-php7.2 libapache2-mod-php  \
php7.2-fpm php7.2-cli php7.2-mysqlnd php7.2-pgsql php7.2-sqlite3 php7.2-redis \
php7.2-apcu php7.2-intl php7.2-imagick php-mcrypt php7.2-json php7.2-gd php7.2-curl \
mcrypt && \
	 rm -rf /var/lib/apt/lists/*
	 
RUN ln -sfn /usr/bin/php7.2 /etc/alternatives/php

RUN a2dismod php5.6

RUN a2enmod proxy_fcgi setenvif
RUN a2enconf php7.2-fpm

RUN a2enmod php7.2
RUN service apache2 restart

CMD ["/run.sh"]
