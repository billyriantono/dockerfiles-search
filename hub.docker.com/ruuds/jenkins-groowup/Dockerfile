FROM jenkins

USER root

RUN apt-get update && apt-get install -y wget git curl libcurl3 zip

RUN apt-get install -y build-essential bison openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libxml2-dev autoconf libc6-dev ncurses-dev automake libtool

RUN curl -sL https://deb.nodesource.com/setup_0.12 | bash -

# Install NPM
RUN apt-get install -y nodejs

# Install Ruby
RUN apt-get install -y ruby-full
RUN gem install rubygems-update
RUN update_rubygems
RUN gem update --system

# Install Compass
RUN gem install compass

# Install grunt-cli
RUN npm install -g grunt-cli

# Install ant
RUN apt-get install -y ant

# Install sudo
RUN apt-get install -y sudo

# Install vim
RUN apt-get install -y vim

# Install PHP5-cli
RUN apt-get install -y php5-cli php5-common php5-curl

# Install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

# Install ttfautohint and fontforge for grunt-webfont
RUN apt-get install -y fontforge ttfautohint

RUN rm -rf /var/lib/apt/lists/*

USER jenkins