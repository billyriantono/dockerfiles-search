FROM ubuntu:18.04
MAINTAINER Damien AUDOUX <damien.audoux@iloh.fr>

# Main installations
RUN apt-get update
RUN apt-get install --yes apt-utils curl gnupg wget
RUN apt-get install --yes gcc g++ make
RUN apt-get install --yes build-essential
RUN curl --silent --location https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install --yes nodejs
RUN apt-get install --yes grunt
RUN apt-get install --yes chrpath libssl-dev libxft-dev libfreetype6 libfreetype6-dev libfontconfig1 libfontconfig1-dev libfontconfig

# Git Installation
RUN apt-get install --yes git
RUN git config --global user.email "contact@iloh.pro"
RUN git config --global user.name "Iloh"

# SSH Configuration
RUN apt-get install --yes sshpass openssh-client

# Chromium
#RUN apt-get install --yes chromium-browser

# Chrome
RUN curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update && apt-get install -y xvfb google-chrome-stable \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV DISPLAY :99.0
ENV CHROME_BIN /usr/bin/google-chrome


# Node and Angular installation
RUN node -v
RUN npm -v
RUN npm install -g @angular/cli
RUN npm install -g findup-sync
RUN npm install -g resolve
RUN npm install -g nopt
RUN npm install -g grunt-known-options
RUN npm install -g grunt-cli

# PhantomJS installation
ENV PHANTOMJS_VERSION 2.1.1
RUN wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-${PHANTOMJS_VERSION}-linux-x86_64.tar.bz2
RUN tar xvjf phantomjs-${PHANTOMJS_VERSION}-linux-x86_64.tar.bz2 -C /usr/local/share/
RUN ln -sf /usr/local/share/phantomjs-${PHANTOMJS_VERSION}-linux-x86_64/bin/phantomjs /usr/local/bin
RUN phantomjs --version




