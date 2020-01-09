FROM webdevops/php-apache:ubuntu-16.04

# Add wkhtmltopdf    
RUN wget http://download.gna.org/wkhtmltopdf/obsolete/linux/wkhtmltopdf-0.10.0_rc1-static-amd64.tar.lzma \
    && tar xf wkhtmltopdf-0.10.0_rc1-static-amd64.tar.lzma \
    && install wkhtmltopdf-amd64 /usr/local/bin/wkhtmltopdf
    
# Add APCu 
# Source: https://launchpad.net/ubuntu/+source/php-apcu/5.1.3+4.0.10-1build1/+build/9538534/+files/php-apcu_5.1.3+4.0.10-1build1_amd64.deb
COPY teufels/	/opt/docker/teufels/
RUN dpkg -i /opt/docker/teufels/apcu/php-apcu_5.1.3+4.0.10-1build1_amd64.deb
RUN echo "extension=apcu.so\napc.enable_cli=1\napc.shm_size = 512M\napc.ttl=7200\napc.user_ttl=7200" > /etc/php/7.0/mods-available/apcu.ini 

#Add Ioncube Loader (beta)
# Source: https://www.ioncube.com/php7-linux-x86-64-beta8.tgz
RUN mkdir -p /usr/local/ioncube \
	&& cp /opt/docker/teufels/ioncube/ioncube_loader_lin_x86-64_7.0b8.so /usr/local/ioncube \
	&& chmod 644 /usr/local/ioncube/ioncube_loader_lin_x86-64_7.0b8.so \
	&& echo "zend_extension = /usr/local/ioncube/ioncube_loader_lin_x86-64_7.0b8.so" > /etc/php/7.0/mods-available/ioncube.ini \
	&& ln -s /etc/php/7.0/mods-available/ioncube.ini /etc/php/7.0/fpm/conf.d/00-ioncube.ini \
	&& ln -s /etc/php/7.0/mods-available/ioncube.ini /etc/php/7.0/cli/conf.d/00-ioncube.ini 