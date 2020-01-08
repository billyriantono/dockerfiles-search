# This Dockerfile is used to build an image containing basic stuff to be used as a Jenkins slave build node.
FROM ubuntu:trusty
MAINTAINER Vitalii Kozytskyi <vitaliikozytskyi@roundforest.com>

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# In case you need proxy
#RUN echo 'Acquire::http::Proxy "http://127.0.0.1:8080";' >> /etc/apt/apt.conf

# Add locales after locale-gen as needed
# Upgrade packages on image
# Preparations for sshd
run locale-gen en_US.UTF-8 &&\
    apt-get -q update &&\
    DEBIAN_FRONTEND="noninteractive" apt-get -q upgrade -y -o Dpkg::Options::="--force-confnew" --no-install-recommends &&\
    DEBIAN_FRONTEND="noninteractive" apt-get -q install -y -o Dpkg::Options::="--force-confnew"  --no-install-recommends openssh-server &&\
    apt-get -q autoremove &&\
    apt-get -q clean -y && rm -rf /var/lib/apt/lists/* && rm -f /var/cache/apt/*.bin &&\
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd &&\
    mkdir -p /var/run/sshd

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get -q update && apt-get install -y build-essential
RUN apt-get install -y openssl libreadline6 libreadline6-dev curl zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev automake libtool bison subversion pkg-config gawk libgmp-dev libgdbm-dev libffi-dev git libpq-dev imagemagick libmagickwand-dev unzip wget libnss3-dev redis-server xvfb curl libcurl4-openssl-dev libfontconfig apt-transport-https
# essential packages for capybara-webkit
RUN apt-get install -y qt5-default libqt5webkit5-dev gstreamer1.0-plugins-base gstreamer1.0-tools gstreamer1.0-x

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list
RUN sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
RUN wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -

RUN apt-get -q update && apt-get install -y google-chrome-stable postgresql-client-9.6

# nvm environment variables
ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 8.4.0

# install nvm
# https://github.com/creationix/nvm#install-script
RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash

# install node and npm
RUN source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

# add node and npm to path so the commands are available
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

RUN curl -o- -L https://yarnpkg.com/install.sh | bash -s -- --version 1.5.1

# install RVM, Ruby, and Bundler
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
RUN curl -L https://get.rvm.io | bash -s stable
RUN echo 'source /etc/profile.d/rvm.sh' >> ~/.bashrc
RUN /usr/local/rvm/bin/rvm-shell -c "rvm requirements"
RUN /bin/bash -l -c "rvm install 2.2.4 && rvm use 2.2.4"
RUN /bin/bash -l -c "rvm install 2.3.0 && rvm use 2.3.0 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.3.2 && rvm use 2.3.2 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.3.3 && rvm use 2.3.3 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.3.4 && rvm use 2.3.4 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.3.7 && rvm use 2.3.7 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.4.0 && rvm use 2.4.0 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.4.1 && rvm use 2.4.1 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.4.2 && rvm use 2.4.2 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.4.3 && rvm use 2.4.3 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.5.0 --disable-binary && rvm use 2.5.0 && gem install bundler --no-ri --no-doc"
RUN /bin/bash -l -c "rvm install 2.5.1 && rvm use 2.5.1 && gem install bundler --no-ri --no-doc"

RUN git config --system user.name Docker && git config --system user.email docker@localhost

# chromedriver

RUN wget http://chromedriver.storage.googleapis.com/2.43/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip
RUN chmod +x chromedriver
RUN mv chromedriver /usr/local/bin
RUN rm /chromedriver_linux64.zip

# phantomjs (remove when chrome 59 with headless will release)
RUN sudo wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN sudo tar xjf phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN sudo mv phantomjs-2.1.1-linux-x86_64 /usr/local/share
RUN sudo ln -s /usr/local/share/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/share/phantomjs
RUN sudo ln -s /usr/local/share/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/bin/phantomjs
RUN rm /phantomjs-2.1.1-linux-x86_64.tar.bz2

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]
