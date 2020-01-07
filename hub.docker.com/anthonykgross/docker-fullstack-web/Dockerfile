FROM anthonykgross/docker-base:ubuntu

MAINTAINER Anthony K GROSS

RUN add-apt-repository ppa:ondrej/php && \
    apt-get update -y && \
	apt-get upgrade -y && \
    apt-get install -y wget curl git php7.1-fpm php7.1-zip php7.1-mysql php7.1-pgsql php7.1-opcache php7.1-xml php7.1-mbstring php7.1-curl php7.1-bcmath php-redis && \
    echo "user = docker" >> /etc/php/7.1/fpm/pool.d/www.conf && \
    service php7.1-fpm start && \
	curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
	apt-get install -y nodejs && \
	php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    chmod a+x composer.phar && \
    mv composer.phar /usr/local/bin/composer && \
    wget http://get.sensiolabs.org/php-cs-fixer.phar -O php-cs-fixer && \
    chmod a+x php-cs-fixer && \
    mv php-cs-fixer /usr/local/bin/php-cs-fixer && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get autoremove -y --purge && \
    npm install -g bower gulp yarn
