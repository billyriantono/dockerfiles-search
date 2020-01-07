FROM debian:stretch
ENV app /var/www
WORKDIR ${app}

RUN apt-get update && \
	apt-get -y install \
		ssh \
		wget \
		git \
		iputils-ping \
		cron \ 
		vim \ 
		apache2 \ 
		php \
		php-zip \
		php-mbstring \
		php-xml \
		php-pgsql \
		php-curl \
		php-gd \
		nfs-common && \
		net-tools && \
		curl && \
	apt-get -y autoremove && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/* && \
	a2enmod ssl rewrite proxy proxy_http proxy_balancer lbmethod_byrequests
	
	
RUN curl -s https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
	curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
	apt-get install nodejs && \
	npm install forever -g

RUN wget https://getcomposer.org/composer.phar && chmod u+x composer.phar && mv composer.phar /usr/local/bin/composer

