FROM centos:centos7.7.1908
MAINTAINER Magecom
# Install required repos, update, and then install PHP-FPM
RUN yum install -y epel-release
RUN yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm
RUN curl --silent --location https://rpm.nodesource.com/setup_10.x | bash -
RUN yum -y update; yum clean all
RUN adduser apache
RUN yum install ImageMagick ImageMagick-devel -y
RUN yum -y install --enablerepo=remi-php71 \
                    php \
                    php-soap \
                    php-pdo \
                    php-mysqlnd \ 
                    php-opcache \
                    php-xdebug \
                    php-xml \ 
                    php-mbstring \ 
                    php-json \
                    php-mcrypt \
                    php-gd \
                    php-devel \
                    php-mysql \
                    php-bcmath \
                    php-intl \
                    php-soap \
                    php-fpm \
                    php-imagick \
                    php-sodium \
                    php-zip \
                git postfix sudo mysql cronie wget openssl-devel zip bzip2 net-tools mhash mc vim nano which ntp psmisc nodejs patch
RUN npm install -g grunt gulp gulp-cli requirejs 
# Install composer
RUN php -r "readfile('https://getcomposer.org/installer');" | php
RUN mv composer.phar /usr/bin/composer
RUN cd /usr/local/bin/ && wget https://files.magerun.net/n98-magerun2.phar && chmod +x /usr/local/bin/n98-magerun2.phar
RUN cd /usr/local/bin/ && wget https://files.magerun.net/n98-magerun.phar && chmod +x /usr/local/bin/n98-magerun.phar
#### Configure and secure PHP
#add scripts
ADD phpfpm_restart.sh /phpfpm_restart.sh
ADD start.sh /start.sh
ADD ioncube.so /usr/lib64/php/modules/ioncube.so
RUN chmod +x /start.sh /phpfpm_restart.sh 
RUN sed -i "s/;date.timezone =.*/date.timezone = Europe\/Kiev/" /etc/php.ini && \
    sed -i "s/user =.*/user = apache/" /etc/php-fpm.d/www.conf && \
    sed -i "s/group =.*/group = apache/" /etc/php-fpm.d/www.conf && \
    sed -i "s/memory_limit = .*/memory_limit = 2G/" /etc/php.ini && \
    sed -i '/^post_max_size = /cpost_max_size = 40M' /etc/php.ini && \
    sed -i '/^upload_max_filesize = /cupload_max_filesize = 40M' /etc/php.ini && \
    sed -i '/^; max_input_vars = /cmax_input_vars = 100000' /etc/php.ini && \
    sed -i '/^max_input_time = /cmax_input_time = 600' /etc/php.ini && \
    sed -i '/^max_execution_time = /cmax_execution_time = 600' /etc/php.ini && \
    sed -i '/^listen = /clisten = 0.0.0.0:9000' /etc/php-fpm.d/www.conf && \
    sed -i '/pid =/s/^/;/g' /etc/php-fpm.conf && \
    sed -i '/^listen.allowed_clients/c;listen.allowed_clients =' /etc/php-fpm.d/www.conf && \ 
    sed -i '/\/var\/lib\/php\/fpm\/session/cphp_value\[session\.save_path\] =\/tmp' /etc/php-fpm.d/www.conf && \
    echo 'xdebug.remote_enable=1' >> /etc/php.d/15-xdebug.ini && \
    echo 'xdebug.idekey="PHPSTORM"' >> /etc/php.d/15-xdebug.ini && \
    echo 'xdebug.remote_port=9001' >> /etc/php.d/15-xdebug.ini && \
    echo 'xdebug.remote_autostart=1' >> /etc/php.d/15-xdebug.ini && \
    echo 'xdebug.remote_connect_back=1' >> /etc/php.d/15-xdebug.ini && \
    echo 'xdebug.remote_host=172.17.0.1' >> /etc/php.d/15-xdebug.ini && \
    echo 'zend_extension = /usr/lib64/php/modules/ioncube.so' >/etc/php.d/10-ioncube.ini && \
    sed -i '/^inet_interfaces = /cinet_interfaces = 127.0.0.1' /etc/postfix/main.cf
RUN ln -s /phpfpm_restart.sh /usr/bin/phpfpm_restart
WORKDIR /var/www
RUN echo '%apache ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
# Set TERM env to avoid error message "TERM environment variable not set" 
ENV TERM xterm
USER apache
#### PORTS
EXPOSE 9000
CMD ["/start.sh"]
