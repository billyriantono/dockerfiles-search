FROM ubuntu:rolling

MAINTAINER pdeleon@pepperminttech.com

ARG USER=percy

ARG UID=1000

RUN useradd -m $USER -s /bin/bash -u $UID 

ADD get_composer /home/$USER

RUN apt-get update && \
 	DEBIAN_FRONTEND=noninteractive && \
 	apt install -y curl zip bzip2 openssl git  && \
	apt-get install -y software-properties-common python-software-properties && \
    LC_ALL=C.UTF-8 add-apt-repository -y -u ppa:ondrej/php && \
	apt-get install -y \
		php7.1 \
		php7.1-fpm \
		php7.1-bcmath \
		php7.1-bz2 \
		php7.1-cli \
		php7.1-common \
		php7.1-curl \
		php7.1-dba \
		php7.1-pdo  \
		php7.1-gd \
		php7.1-gmp \
		# php7.1-imap \
		# php7.1-intl \
		# php7.1-ldap \
		php7.1-mbstring \
		php7.1-mcrypt \
		php7.1-mysql \
		# php7.1-recode \
		# php7.1-snmp \
		php7.1-soap \
		php7.1-sqlite \
		php7.1-tidy \
		php7.1-xml \
		php7.1-xmlrpc \
		php7.1-xsl \
		php7.1-zip && \
	su - $USER -c "/bin/bash /home/$USER/get_composer" && \
	cp -pv /home/$USER/composer.phar /usr/local/bin/composer && \
	su - $USER -c "php /home/$USER/composer.phar global require laravel/installer" && \
	su - $USER -c "echo export PATH=\$PATH:\$HOME/.composer/vendor/bin >> /home/$USER/.bashrc" && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /home/$USER/composer.phar && \
	rm -rf /home/$USER/get_composer
