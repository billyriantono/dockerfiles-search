FROM phusion/baseimage:0.9.18
MAINTAINER Harsh Vakharia <harshjv@gmail.com>
MAINTAINER Leandro Banchio <lbanchio@gmail.com>
MAINTAINER Emiliano Rodriguez <emiliano.rodriguez26@gmail.com>

# Default baseimage settings
ENV HOME /root
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh
CMD ["/sbin/my_init"]
ENV DEBIAN_FRONTEND noninteractive

# Update software list, install php-nginx & clear cache
RUN locale-gen en_US.UTF-8 && \
    export LANG=en_US.UTF-8 && \
    add-apt-repository -y ppa:ondrej/php && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --force-yes nginx \
    php7.2-zip php7.2-fpm php7.2-mysql php7.2-redis \
    php7.2-imagick php7.2-xdebug php7.2-apcu php7.2-xml \
    php7.2-sqlite3 php-mbstring git \
    php7.2-curl php7.2-gd php7.2-intl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* \
           /tmp/* \
           /var/tmp/*

# Configure nginx
RUN echo "daemon off;" >>                                               /etc/nginx/nginx.conf
RUN sed -i "s/sendfile on/sendfile off/"                                /etc/nginx/nginx.conf
RUN mkdir -p                                                            /var/www

# Configure PHP
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/"                  /etc/php/7.2/fpm/php.ini
RUN sed -i -e "s/;daemonize\s*=\s*yes/daemonize = no/g"                 /etc/php/7.2/fpm/php-fpm.conf
##For dev enviroment
RUN sed -i 's/display_errors =.*/display_errors = On/g'                 /etc/php/7.2/fpm/php.ini
RUN sed -i 's/display_startup_errors =.*/display_startup_errors = On/g' /etc/php/7.2/fpm/php.ini
RUN sed -i 's/upload_max_filesize =.*/upload_max_filesize = 64M/g'      /etc/php/7.2/fpm/php.ini
###Updated for PHP 7.0
#RUN sed -i "s/pid =.*/pid = \/var\/run\/php-fpm.pid/"                   /etc/php/7.2/fpm/php-fpm.conf
#RUN sed -i "s/listen =.*sock/listen = \/var\/run\/php-fpm.sock/"        /etc/php/7.2/fpm/pool.d/www.conf
###
RUN sed -i "s/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/"                  /etc/php/7.2/cli/php.ini
RUN sed -i "s/date.timezone =.*/date.timezone = America\/Argentina\/Cordoba/g" /etc/php/7.2/fpm/php.ini
RUN phpenmod xdebug
RUN phpenmod zip

# Add nginx service
RUN mkdir                                                               /etc/service/nginx
ADD build/nginx/run.sh                                                  /etc/service/nginx/run
RUN chmod +x                                                            /etc/service/nginx/run

# Add PHP service
RUN mkdir                                                               /etc/service/phpfpm
ADD build/php/run.sh                                                    /etc/service/phpfpm/run
RUN chmod +x                                                            /etc/service/phpfpm/run

# Add nginx
VOLUME ["/var/www", "/etc/nginx/sites-available", "/etc/nginx/sites-enabled"]

# Workdir
WORKDIR /var/www

EXPOSE 80
