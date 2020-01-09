FROM webdevops/php-apache:ubuntu-16.04

RUN mkdir /tmp/ioncube_install
ADD http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz /tmp/ioncube_install/
WORKDIR /tmp/ioncube_install
RUN tar xvfz /tmp/ioncube_install/ioncube_loaders_lin_x86-64.tar.gz && ls -all /tmp/ioncube_install/ \
	&& rm /tmp/ioncube_install/ioncube_loaders_lin_x86-64.tar.gz \
	&& mkdir -p /usr/local/ioncube \
	&& PHP_VERSION=$(php -r "echo PHP_MAJOR_VERSION.'.'.PHP_MINOR_VERSION;") \
	&& cp /tmp/ioncube_install/ioncube/ioncube_loader_lin_${PHP_VERSION}.so /usr/local/ioncube \
	&& rm -rf /tmp/ioncube_install/ioncube \
	&& echo "zend_extension = /usr/local/ioncube/ioncube_loader_lin_${PHP_VERSION}.so" >> /etc/php5/mods-available/ioncube.ini \
	&& ln -s /etc/php5/mods-available/ioncube.ini /etc/php5/fpm/conf.d/00-ioncube.ini
    
RUN wget http://download.gna.org/wkhtmltopdf/obsolete/linux/wkhtmltopdf-0.10.0_rc1-static-amd64.tar.lzma \
    && tar xf wkhtmltopdf-0.10.0_rc1-static-amd64.tar.lzma \
    && install wkhtmltopdf-amd64 /usr/local/bin/wkhtmltopdf
    
# Add APCu 
# Source: https://launchpad.net/ubuntu/+source/php-apcu/4.0.10-1/+build/8417263
COPY teufels/ /opt/docker/teufels/
RUN dpkg -i /opt/docker/teufels/apcu/php5-apcu_4.0.10-1_amd64.deb
RUN echo "extension=apcu.so\napc.shm_size = 512M\napc.ttl=7200\napc.user_ttl=7200\napc.enable_cli=1" >> /etc/php5/mods-available/apcu.ini 