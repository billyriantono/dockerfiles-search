FROM ubuntu:latest
MAINTAINER Ben Blanks <ben@d15k.com>

# Set the timezone to Australia/Sydney
RUN ln -sf /usr/share/zoneinfo/Australia/Sydney /etc/localtime

##
# Install the packages
#
RUN apt-get update --no-install-recommends -y
RUN apt-get install --no-install-recommends -y \
    php5 \
    php5-cli \
    php5-curl \
    php5-dev \
    php5-gd \
    php5-mysqlnd \
    php5-xdebug \
    php5-mcrypt \
    php5-json \
    openssl \
    ca-certificates \
    curl \
    git \
    openssh-client &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/*

##
# Remove the html directory so we have a clean www directory.
#
RUN rm -rf /var/www/html &&\
    rm /etc/apache2/sites-enabled/000-default.conf &&\
    rm /etc/apache2/conf-enabled/other-vhosts-access-log.conf
    
##
# Copy the config files that will be used to override the server defaults.
#
COPY docker/etc/ /etc/

##
# Install the developer toolchain
#
RUN curl -O https://phar.phpunit.de/phpunit.phar &&\
    chmod a+x phpunit.phar &&\
    mv phpunit.phar /usr/local/bin/phpunit

##
# Reconfigure PHP
#
RUN sed -i 's/display_errors = Off/display_errors = On/g' /etc/php5/apache2/php.ini &&\
    sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 102M/g' /etc/php5/apache2/php.ini &&\
    sed -i 's/post_max_size = 8M/post_max_size = 108M/g' /etc/php5/apache2/php.ini &&\
    sed -i 's/;date.timezone =/date.timezone = "Australia\/Sydney"/g' /etc/php5/apache2/php.ini &&\
    php5enmod mcrypt


##
# Configure Apache
#
RUN a2enmod headers rewrite ssl

EXPOSE 80 443

VOLUME ["/var/www/"]
WORKDIR /var/www/

##
# Add a user for the files from the host machine to belong to, 
# also so that the user can be logged into for things such as
# - Unit Testing
# - Debugging
# - Etc
#
RUN useradd www

##
# Add the public key to the authorized file for the www user so root 
# can login without a password.
#
RUN echo -e  'y\n' | ssh-keygen -q -t rsa -N "" -f ~/.ssh/id_rsa
RUN mkdir -p /home/www/.ssh &&\
    chown www:www /home/www/.ssh &&\
    chmod 0700 /home/www/.ssh &&\
    cat ~/.ssh/id_rsa.pub >> /home/www/.ssh/authorized_keys &&\
    chown www:www /home/www/.ssh/authorized_keys &&\
    chmod 0600 /home/www/.ssh/authorized_keys
    
    
