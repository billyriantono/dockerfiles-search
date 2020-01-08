FROM ubuntu:17.04
USER root

# ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

# Utils
RUN apt-get update; \
    apt-get -y install \
        software-properties-common \
        python-software-properties \
        language-pack-en-base \
        apt-utils \
        man-db \
        sudo \
        autoconf \
        build-essential \
        curl \
        openssl \
        ca-certificates \
        git \
        make \
        nano \
        vim \
        tree \
        strace \
        telnet \
        htop \
        wget \
        zip \
        # unzip \
        ruby-full \
        w3m \
        supervisor \
        libssl-dev \
        zlib1g-dev \
        libjpeg-dev \
        libtiff-dev \
        libpng-dev \
        libnotify-bin \
        libsodium-dev

# Node 6 > Node 7
RUN apt-get install -y \
        nodejs \
        npm; \
    curl -sL https://deb.nodesource.com/setup_7.x | bash -; \
    apt-get install -y nodejs; \
    npm cache clear

# Bower, Babel Cli, Grunt Cli, Gulp Cli, Minimatch, JsHint
RUN npm install -g \
        node-gyp \
        bower \
        bower-update-all \
        babel-cli \
        grunt-cli \
        gulp-cli \
        minimatch \
        marked \
        jshint

# Git completion
RUN curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash

# Make /app directory
ENV APP_DIR /app
ENV GIT_DIR ${APP_DIR}
ENV APP_STORAGE_DIR ${APP_DIR}/storage
RUN mkdir ${APP_DIR}; \
    chown ${ADMIN_USER}:${ADMIN_GROUP} ${APP_DIR}; \
    chmod 775 ${APP_DIR}

# Admin user
ENV ADMIN_GROUP admin
ENV ADMIN_USER  admin
ENV ADMIN_GID   22999
ENV ADMIN_UID   22999
ENV ADMIN_HOME  /home/${ADMIN_USER}
RUN \
    groupadd -g ${ADMIN_GID} ${ADMIN_GROUP}; \
    useradd -d ${ADMIN_HOME} -s /bin/bash -g ${ADMIN_GROUP} -u ${ADMIN_UID} ${ADMIN_USER}; \
    mkdir ${ADMIN_HOME}; \
    chown ${ADMIN_USER}:${ADMIN_GROUP} ${ADMIN_HOME}; \
    chmod 700 ${ADMIN_HOME}

# Make /admin directory
ENV ADMIN_DIR /admin
ENV ADMIN_SCRIPTS /admin/scripts
RUN mkdir ${ADMIN_DIR}
COPY admin /admin
RUN chown -R ${ADMIN_USER}:${ADMIN_GROUP} ${ADMIN_DIR}; \
    chmod 770 ${ADMIN_DIR}; \
    chmod 770 $(find ${ADMIN_SCRIPTS} -type f)

# Logger user
ENV LOGGER_GROUP logger
ENV LOGGER_USER  logger
ENV LOGGER_GID   23000
ENV LOGGER_UID   23000
ENV LOGGER_HOME  /home/${LOGGER_USER}
RUN \
    groupadd -g ${LOGGER_GID} ${LOGGER_GROUP}; \
    useradd -d ${LOGGER_HOME} -s /bin/bash -g ${LOGGER_GROUP} -u ${LOGGER_UID} ${LOGGER_USER}; \
    mkdir ${LOGGER_HOME}; \
    chown ${LOGGER_USER}:${LOGGER_GROUP} ${LOGGER_HOME}; \
    chmod 700 ${LOGGER_HOME}

# Make /log directory
ENV LOG_DIR /log
RUN mkdir ${LOG_DIR}; \
    chown ${LOGGER_USER}:${LOGGER_GROUP} ${LOG_DIR}; \
    chmod 770 ${LOG_DIR}

# Runner user
ENV RUNNER_GROUP runner
ENV RUNNER_USER  runner
ENV RUNNER_GID   24000
ENV RUNNER_UID   24000
ENV RUNNER_HOME  /home/${RUNNER_USER}
RUN \
    groupadd -g ${RUNNER_GID} ${RUNNER_GROUP}; \
    useradd -d ${RUNNER_HOME} -s /bin/bash -g ${RUNNER_GROUP} -u ${RUNNER_UID} ${RUNNER_USER}; \
    mkdir ${RUNNER_HOME}; \
    chown ${RUNNER_USER}:${RUNNER_GROUP} ${RUNNER_HOME}; \
    chmod 700 ${RUNNER_HOME}

# Runner home
COPY home/runner ${RUNNER_HOME}
RUN cd ${RUNNER_HOME}; \
    chown ${RUNNER_USER}:${RUNNER_GROUP} sleep.sh; \
    chmod 500 sleep.sh; \
    chmod +x sleep.sh; \
    chmod 500 php/db-connect-test.php

# Developer user
ENV DEVELOPER_GROUP developer
ENV DEVELOPER_USER  developer
ENV DEVELOPER_GID   25000
ENV DEVELOPER_UID   25000
ENV DEVELOPER_HOME  /home/${DEVELOPER_USER}
RUN \
    groupadd -g ${DEVELOPER_GID} ${DEVELOPER_GROUP}; \
    useradd -d ${DEVELOPER_HOME} -s /bin/bash -g ${DEVELOPER_GROUP} -u ${DEVELOPER_UID} ${DEVELOPER_USER}; \
    mkdir ${DEVELOPER_HOME}; \
    chown ${DEVELOPER_USER}:${DEVELOPER_GROUP} ${DEVELOPER_HOME}; \
    chmod 700 ${DEVELOPER_HOME}; \
    usermod -a -G ${ADMIN_GROUP} ${DEVELOPER_USER}

# Set Apache environment
ENV APACHE_GROUP www-data
ENV APACHE_USER www-data
ENV APACHE_GID 1000
ENV APACHE_UID 1000
ENV APACHE_HOME /home/www-data
ENV APACHE_RUN_USER ${APACHE_USER}
ENV APACHE_RUN_GROUP ${APACHE_GROUP}
ENV APACHE_LOG_DIR ${LOG_DIR}
ENV APACHE_ERROR_LOG ${LOG_DIR}/error.log
ENV APACHE_ACCESS_LOG ${LOG_DIR}/access.log

# Apache user
RUN usermod -u ${APACHE_UID} ${APACHE_USER}; \
    groupmod -g ${APACHE_GID} ${APACHE_GROUP}; \
    mkdir ${APACHE_HOME}; \
    chown ${APACHE_USER}:${APACHE_GROUP} ${APACHE_HOME}; \
    chmod 700 ${APACHE_HOME}; \
    usermod -a -G ${APACHE_GROUP} ${ADMIN_USER}; \
    usermod -a -G ${APACHE_GROUP} ${RUNNER_USER}; \
    usermod -a -G ${APACHE_GROUP} ${DEVELOPER_USER}; \
    usermod -a -G ${LOGGER_GROUP} ${APACHE_USER}

# Composer home
ENV COMPOSER_HOME ${ADMIN_DIR}/.composer
RUN mkdir ${COMPOSER_HOME}; \
    chown ${ADMIN_USER}:${ADMIN_GROUP} ${COMPOSER_HOME}; \
    chmod 770 ${COMPOSER_HOME}
ENV PATH ${COMPOSER_HOME}/vendor/bin:$PATH

# Npm cache
ENV NPM_DIR ${ADMIN_DIR}/.npm
ENV NPM_CACHE ${NPM_DIR}/cache
RUN mkdir ${NPM_DIR}; \
    mkdir ${NPM_CACHE}; \
    chown -R ${ADMIN_USER}:${ADMIN_GROUP} ${NPM_CACHE}
RUN npm config --global set prefix ${NPM_DIR}; \
    npm config --global set cache ${NPM_CACHE}

# Copy sudoers configuration file
USER root
COPY etc/ /etc/ 
RUN chown root:root    /etc/sudoers; \
    chmod 750          /etc/sudoers; \
    chown -R root:root /etc/sudoers.d; \
    chmod 440 $(find /etc/sudoers.d -type f)

# Configure the executable
# ENV SERVER_ENV local
WORKDIR /
ENTRYPOINT ["/bin/true"]
CMD []
LABEL name Ubuntu/17.04" description Ubuntu 17.04"
MAINTAINER docker@ericmugerwa.com
