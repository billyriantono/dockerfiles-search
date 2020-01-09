#Using Ubuntu latest image
FROM ubuntu

# Author of this Script
MAINTAINER ag.sampath

# Install dependancies 
RUN apt-get update && apt-get install -y software-properties-common python-software-properties
RUN LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php

# Install web Server 
RUN apt-get update && apt-get install -y nginx

# Install PHP 7 and related modules
RUN apt-get install -y php7.2 php7.2-curl php7.2-mysql php7.2-mbstring php7.2-gd

# home directory
WORKDIR /var/www/html

# Adding local files to directory in docker
ADD assets/. /var/www/html/assets
# Mounting Local directory as Volume in Docker image
VOLUME /var/www/html/assets

# Start the Nginx service while creating container
CMD service nginx start
