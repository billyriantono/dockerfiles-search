FROM jenkins:latest


# -----------------------------------------------------
# Lines below are from allansun/birdsystem-development
# -----------------------------------------------------

# This Dockerfile is intended for development purpose only
# It uses root as apache user to prevent synced folder permission issue 
MAINTAINER Allan Sun <allan.sun@bricre.com>

USER root 
WORKDIR /home

# Manually set up the apache environment variables
ENV APACHE_RUN_USER root
ENV APACHE_RUN_GROUP root
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_SERVERNAME localhost

# Update apt-get to make sure we get latest repos
RUN apt-get update 
RUN apt-get -y upgrade 

# Install apt-transport-https...
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apt-transport-https

# Add Docker GPG Key & Repo & update aga
RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo "deb https://apt.dockerproject.org/repo debian-jessie main" > /etc/apt/sources.list.d/docker.list
RUN apt-get update

# Install apache, PHP, and supplimentary programs. curl and lynx-cur are for debugging the container.
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install locales apache2 php5 php5-cli php5-dev php5-mcrypt libapache2-mod-php5 php5-mysql php5-gd php-pear php-apc php5-curl php5-xsl curl lynx lynx-cur vim htop wget

# Instal composer and other PHP essential libraries
RUN curl -sS "https://getcomposer.org/installer" | php -- --install-dir=/usr/local/bin --filename=composer && \
	composer global require 'phploc/phploc=*' && \
	composer global require "phpunit/phpunit=4.3.*" && \
	composer global require "pdepend/pdepend=2.0.*" && \
	composer global require "phpmd/phpmd=@stable" && \
	composer global require "sebastian/phpcpd=*" && \ 
	wget http://phpdox.de/releases/phpdox.phar  && chmod +x phpdox.phar && mv phpdox.phar /root/.composer/vendor/bin/ && \

	pear install PHP_CodeSniffer

RUN echo "PATH=$PATH:/root/.composer/vendor/bin" >> /root/.profile

RUN pecl install xdebug
RUN echo 'zend_extension="/usr/lib/php5/20131226/xdebug.so"' >> /etc/php5/apache2/php.ini && \
	echo 'zend_extension="/usr/lib/php5/20131226/xdebug.so"' >> /etc/php5/cli/php.ini 

# Update the default apache site with the config we created.
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf

# Ensure mod_rewrite is enabled
RUN a2enmod rewrite 

# Configure timezone and locale
RUN echo "Europe/London" > /etc/timezone; dpkg-reconfigure -f noninteractive tzdata 
RUN export LANGUAGE=en_US.UTF-8; export LANG=en_US.UTF-8; export LC_ALL=en_US.UTF-8; locale-gen en_US.UTF-8; DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales 

# Install Zend Framework 
RUN wget https://packages.zendframework.com/releases/ZendFramework-1.12.9/ZendFramework-1.12.9.tar.gz 
RUN tar -xzf ZendFramework-1.12.9.tar.gz -C /home/ 
RUN rm -f ZendFramework-1.12.9.tar.gz 
RUN pear install Image_Text-beta

# Install Docker
RUN DEBIAN_FRONTEND=noninteractive apt-get install --yes docker-engine
RUN useradd -g jenkins docker

# php.ini settings
RUN sed -i 's/\;date\.timezone\ \=/date\.timezone\ \=\ Europe\/London/g' /etc/php5/apache2/php.ini && \
sed -i "s/;include_path = \"\.:.*/include_path = \".:\/usr\/share\/php:\/home\/ZendFramework-1.12.9\/library\"/" /etc/php5/apache2/php.ini && \
sed -i "s/error_reporting = .*$/error_reporting = E_ALL \& ~E_NOTICE \& ~E_STRICT \& ~E_DEPRECATED/" /etc/php5/apache2/php.ini && \
sed -i 's/\;date\.timezone\ \=/date\.timezone\ \=\ Europe\/London/g' /etc/php5/cli/php.ini && \
sed -i "s/;include_path = \"\.:.*/include_path = \".:\/usr\/share\/php:\/home\/ZendFramework-1.12.9\/library\"/" /etc/php5/cli/php.ini && \
sed -i "s/error_reporting = .*$/error_reporting = E_ALL \& ~E_NOTICE \& ~E_STRICT \& ~E_DEPRECATED/" /etc/php5/cli/php.ini

EXPOSE 8080

WORKDIR /var/www/html

# -----------------------------------------------------
# Lines below are for birdsystem/jenkins only
# -----------------------------------------------------
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install ant sudo mysql-client

USER jenkins

COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt
