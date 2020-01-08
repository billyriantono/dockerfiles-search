###########################################################
# Dockerfile Ubuntu 16.xx  PHP 7.x
# Based on: ubuntu:latest
# DATE: 05/12/2016
############################################################

# Set the base image to Ubuntu 14.04 latest
FROM ubuntu:xenial

# File Author / Maintainer
MAINTAINER Mathias Åsberg mathias.asberg@gmail.com
ARG DEBIAN_FRONTEND=noninteractive
###################################################################
#  UPDATES & PRE-REQS  ******
###################################################################

RUN apt-get clean all && apt-get update && apt-get -y upgrade && apt-get install -y \
    apache2 \
    apache2-utils \
    curl \
    php7.0 \
    libapache2-mod-php7.0 \
    php7.0-cli \
    php7.0-common \
    php7.0-curl \
    php7.0-gd \
    php7.0-xml \
    php7.0-mysql \
    vim \
    unzip wget git \

&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*


RUN service apache2 restart


###################################################################
#****  Reset Apache CTN
###################################################################

# This section will handle undoing any install magic that the apache base container did on setup.
RUN rm -fr /etc/apache2/sites-available/apache_deb.conf && \
    rm -fr /var/www/*; mkdir -p /var/www/html && \
    rm -fr /tmp/install.log && \
    chown -R www-data:www-data /var/www/html && \
    ls -lah /var/www


###################################################################
#  POST DEPLOY CLEAN UP  ******
###################################################################

VOLUME /var/www/html

RUN chown -R www-data:www-data /var/www


###################################################################
#  CONFIGURE START ITEMS  *******
###################################################################

ENV TERM xterm

# Set up Data Volume and Set docker run command.
CMD /bin/bash -c "service apache2 stop && /usr/sbin/apache2ctl -D FOREGROUND"






