FROM php:cli-stretch

RUN apt-get update && apt-get install -yqq --no-install-recommends \
      curl \
      gnupg2 \
      dirmngr \
      git \
      zip \
      unzip

# NodeJS repo
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

# Ansible repo
RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" >> /etc/apt/sources.list.d/ansible.list && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367

# Install nodejs & ansible
RUN apt-get update -yqq && apt-get install -yqq --no-install-recommends \
      ansible \
      nodejs

# Composer
COPY --from=composer:latest /usr/bin/composer usr/bin/composer
RUN composer global require hirak/prestissimo

RUN useradd -ms /bin/bash deployer

USER deployer
