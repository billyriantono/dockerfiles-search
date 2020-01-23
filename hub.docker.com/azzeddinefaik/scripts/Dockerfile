FROM ubuntu:14.04

MAINTAINER Anmol Nagpal <anmol.nagpal@tajawal.com>

# Keep upstart from complaining
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -sf /bin/true /sbin/initctl

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive
RUN export LANG=C.UTF-8

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install  software-properties-common python-software-properties

# Nginx
RUN sudo add-apt-repository ppa:nginx/stable

# php
RUN export LANG=C.UTF-8 && sudo add-apt-repository ppa:ondrej/php


RUN apt-get -y update

RUN sudo apt-get -y install  pwgen python-setuptools curl git unzip vim \
            openssl git git-core htop rsyslog zip vim-common multitail sysvbanner figlet python-pip zsh wget telnet libpcre3 libpcre3-dev ssh

RUN apt-get -y install nodejs
RUN apt-get install -y openssh-server

#Nodejs 7.2.1
RUN set -ex \
  && for key in \
    9554F04D7259F04124DE6B476D5A82AC7E37093B \
    94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
    0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
    FD3A5288F042B6850C66B31F09FE44734EB7990E \
    71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
    DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
    B9AE9905FFD7803F25714661B63B535A4C206CA9 \
    C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
  ; do \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys "$key"; \
  done

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 7.2.1

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.xz" \
  && curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
  && gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc \
  && grep " node-v$NODE_VERSION-linux-x64.tar.xz\$" SHASUMS256.txt | sha256sum -c - \
  && tar -xJf "node-v$NODE_VERSION-linux-x64.tar.xz" -C /usr/local --strip-components=1 \
  && rm "node-v$NODE_VERSION-linux-x64.tar.xz" SHASUMS256.txt.asc SHASUMS256.txt \
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs

RUN npm install -g pm2

RUN pip install awscli

RUN mkdir -p /var/run/sshd
# Supervisor Config

RUN sudo useradd ubuntu
RUN passwd -d ubuntu
RUN passwd -d root
RUN echo "PermitEmptyPasswords yes" >> /etc/ssh/sshd_config
RUN echo "ubuntu ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN echo "ChallengeResponseAuthentication no" >> /etc/ssh/sshd_config
RUN echo "PubkeyAuthentication yes" >> /etc/ssh/sshd_config
RUN chsh -s `which bash` ubuntu
RUN usermod -d /home/ubuntu ubuntu
RUN mkdir -p /home/ubuntu
RUN ssh-keygen -t rsa1 -f /etc/ssh/ssh_host_rsa_key -y
RUN ssh-keygen -t dsa  -f /etc/ssh/ssh_host_dsa_key -y
RUN mkdir -p /home/ubuntu/.ssh
RUN chmod 755 /home/ubuntu/.ssh
ADD ./id_rsa /home/ubuntu/.ssh/authorized_keys
RUN chmod 600 /home/ubuntu/.ssh/authorized_keys
RUN chown -R ubuntu:ubuntu /home/ubuntu
RUN chmod 755 /home/ubuntu
# Install zsh
ADD ./files/install-zsh.sh /root/install-zsh.sh
ADD ./files/install-zsh.sh /home/ubuntu/install-zsh.sh

RUN chmod +x /root/install-zsh.sh
RUN chmod +x /home/ubuntu/install-zsh.sh
RUN sh /root/install-zsh.sh

RUN su - ubuntu -c "sh /home/ubuntu/install-zsh.sh"

#RUN echo 'root:p' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN rm  /root/.zshrc
ADD ./files/zshrc /root/.zshrc
ADD ./files/zshrc /home/ubuntu/.zshrc

RUN chsh -s `which zsh` ubuntu
RUN chsh -s `which zsh`

RUN chmod -R 755 /usr/local/share/zsh/site-functions

RUN apt-get -y install \
        php7.1-fpm   \
        php7.1   \
        php7.1-common   \
        php7.1-cli   \
        php7.1-curl   \
        php7.1-gd   \
        php7.1-gmp   \
        php7.1-imap   \
        php7.1-interbase   \
        php7.1-intl   \
        php7.1-mcrypt   \
        php7.1-readline   \
        php7.1-tidy   \
        php7.1-xmlrpc   \
        php7.1-xsl   \
        php7.1-json   \
        php7.1-mysql   \
        php7.1-opcache   \
        php7.1-xdebug    \
        php-apcu   \
        php-redis    \
        php-apcu-bc   \
        php-amqp   \
        php7.1-bz2   \
        php7.1-bcmath    \
        php7.1-mbstring    \
        php7.1-soap   \
        php7.1-xml   \
        php7.1-zip   \
        php-pear   \
        php-mongodb \
        php7.1-dev

# Allow Composer to be run as root
ENV COMPOSER_ALLOW_SUPERUSER 1
# Register the COMPOSER_HOME environment variable
ENV COMPOSER_HOME /home/ubuntu/.composer
# Add global binary directory to PATH and make sure to re-export it
ENV PATH /home/ubuntu/.composer/vendor/bin:$PATH

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer self-update

# install global php tools
RUN composer global require phpunit/phpunit \
        phpunit/phpunit-mock-objects \
        phpmetrics/phpmetrics \
        squizlabs/php_codesniffer \
        pdepend/pdepend \
        phpmd/phpmd \
        jakub-onderka/php-parallel-lint

RUN composer global update

#java
RUN apt-get update
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update

ADD ./files/xdebug.ini /etc/php/7.1/mods-available/xdebug.ini

# automatically accept oracle license
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
# and install java 8 oracle jdk
RUN apt-get -y install oracle-java8-installer && apt-get clean
RUN update-alternatives --display java
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Define default command.
EXPOSE 22
