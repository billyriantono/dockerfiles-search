#
# Create the container for Magento with Magento memory requirements
#

FROM m2i3/nginx-php5:latest
MAINTAINER Jean-Marc Lagace <jean-marc@m2i3.com>


ENV MAGE_RUN_CODE="default" MAGE_RUN_TYPE="store"

RUN pear install Net_GeoIP


# reduce the number of processes running at once 
RUN sed -i -e 's/^worker_processes .*;/worker_processes 1;/' /etc/nginx/nginx.conf
RUN sed -i -e 's/worker_connections .*;/worker_connections 2048;/' /etc/nginx/nginx.conf

# change default memory allocation to requirements by Magento 
RUN sed -i -e 's/^memory_limit = .*/memory_limit = 512M/' /etc/php5/fpm/php.ini
RUN sed -i -e 's/^upload_max_filesize = .*/upload_max_filesize = 15M/' /etc/php5/fpm/php.ini
RUN sed -i -e 's/^post_max_size = .*/post_max_size = 15M/' /etc/php5/fpm/php.ini

# make php-fpm a bit more tight
RUN sed -i -e 's/^pm.max_children = .*/pm.max_children = 100/' /etc/php5/fpm/pool.d/www.conf
RUN sed -i -e 's/^;pm.max_requests = .*/pm.max_requests = 500/' /etc/php5/fpm/pool.d/www.conf

RUN sed -i -e 's/^;emergency_restart_threshold = .*/emergency_restart_threshold = 20/' /etc/php5/fpm/php-fpm.conf 

ADD nginx-site.conf /etc/nginx/sites-available/default
ADD 500-setenvironment.sh /usr/lib/startup.d/
RUN chmod +x /usr/lib/startup.d/*
EXPOSE 80

