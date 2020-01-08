FROM ubuntu:14.04

MAINTAINER Denis Andrejew <da.colonel@gmail.com>

# curl, wget etc
RUN apt-get update -qq && apt-get install -y -qq git curl wget

# HHVM
RUN wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | apt-key add -
RUN echo deb http://dl.hhvm.com/ubuntu trusty main | tee /etc/apt/sources.list.d/hhvm.list
RUN apt-get update -qq && apt-get install -y -qq hhvm

# composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer

# all done? clean up!
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
