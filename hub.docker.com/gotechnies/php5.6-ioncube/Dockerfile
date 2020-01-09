FROM ubuntu:latest
MAINTAINER Arvind Rawat (arvindr226@gmail.com)

# install dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    software-properties-common
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php 
RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		apache2 \
		ca-certificates openssl \
		curl \
		php5.6 \
		php5.6-curl \
		php5.6-gd \
		php5.6-json \
		php5.6-simplexml \
		php5.6-mbstring \
		php5.6-mysql \
		php5.6-zip \
		openssh-server \
		composer \
		php5.6-mcrypt \
		php5.6-intl \
                supervisor  \
		libapache2-mod-php5.6 \
	&& rm -r /var/lib/apt/lists/*
RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride All/' /etc/apache2/apache2.conf
RUN a2enmod rewrite expires
RUN a2enmod ssl
RUN a2enmod headers
WORKDIR /opt
RUN curl -O http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz
RUN tar -xvf ioncube*.tar.gz
RUN cp ioncube/* /usr/lib/php/20131226/
RUN echo "zend_extension = /usr/lib/php/20131226/ioncube_loader_lin_5.6.so" >> /etc/php/5.6/apache2/php.ini 
RUN mkdir /var/run/sshd
RUN echo 'root:screencast' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN  sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/g' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
## Mount ##
WORKDIR /var/www/html
VOLUME /var/www/html
# Default command	
#CMD ["apachectl", "-D", "FOREGROUND"] 
# Ports
EXPOSE 80
EXPOSE 443
EXPOSE 22
CMD ["/usr/bin/supervisord"]
