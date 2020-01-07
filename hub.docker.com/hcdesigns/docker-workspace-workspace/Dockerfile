FROM phusion/baseimage:latest

LABEL maintainer="Harvey Chow <harvey@hcdesigns.nl>"

RUN DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y \
        curl \
        locales \
        software-properties-common \
        python-software-properties \
        pkg-config \
        libcurl4-openssl-dev \
        libedit-dev \
        libssl-dev \
        libxml2-dev \
        xz-utils \
        git \
        vim \
        nano \
        mysql-client

#####################################
# Install python (required for several npm builds)
#####################################
RUN apt-get install -y python

#####################################
# Set locales and set timezone
#####################################
RUN locale-gen en_US.UTF-8

ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LC_CTYPE=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV TERM xterm

RUN ln -snf /usr/share/zoneinfo/CEST /etc/localtime && echo CEST > /etc/timezone

#####################################
# PHP 5.6
#####################################
RUN add-apt-repository ppa:ondrej/php && \
    apt-get update

# Install "PHP Extentions", "libraries", "Software's"
RUN apt-get install -y  \
        php5.6-cli \
        php5.6-common \
        php5.6-curl \
        php5.6-intl \
        php5.6-json \
        php5.6-xml \
        php5.6-mbstring \
        php5.6-mcrypt \
        php5.6-mysql \
        php5.6-zip \
        php5.6-bcmath \
        php5.6-memcached \
        php5.6-gd \
        php5.6-dev \
        php5.6-soap

#####################################
# Non-Root User:
#####################################
# Add a non-root user to prevent files being created with root permissions on host machine.
ENV PUID 1000
ENV PGID 1000

RUN groupadd -g ${PGID} hcdesigns && \
    useradd -u ${PUID} -g hcdesigns -m hcdesigns

#####################################
# Python, NodeJS, yarn
#####################################
RUN curl -sL https://deb.nodesource.com/setup_9.x | bash - &&\
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - &&\
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update && \
    apt-get install -y nodejs yarn

#####################################
# Magerun for Magento 1 & 2
#####################################
# Magerun magento 1
RUN curl -sL -O https://files.magerun.net/n98-magerun.phar &&\
    chmod +x ./n98-magerun.phar && \
    mv ./n98-magerun.phar magerun && \
    mv magerun /usr/bin/

# Magerun magento 2
RUN curl -sL -O https://files.magerun.net/n98-magerun2.phar &&\
    chmod +x ./n98-magerun2.phar &&\
    mv ./n98-magerun2.phar magerun2 &&\
    mv ./magerun2 /usr/bin/

#
#--------------------------------------------------------------------------
# Final Touch
#--------------------------------------------------------------------------
#

# Clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set default work directory
WORKDIR /var/www