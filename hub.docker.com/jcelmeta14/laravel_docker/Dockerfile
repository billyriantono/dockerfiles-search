FROM ubuntu:18.04

ENV NVM_DIR=/home/docker/.nvm
ENV NODE_VERSION=v12.13.0
ENV NODE_PATH=$NVM_DIR/versions/node/$NODE_VERSION/lib/node_modules

ENV COMPOSER_HOME=/home/docker/.composer

ENV PATH=$NVM_DIR/versions/node/$NODE_VERSION/bin:$COMPOSER_HOME/vendor/bin:$PATH

ENV LANG="en_US.UTF-8"
ENV LANGUAGE="en_US.UTF-8"
ENV LC_ALL="en_US.UTF-8"

ARG git-user="Jurgen Çelmeta"
ARG git-email="jur.celmeta@gmail.com"
ARG tz="Europe/Tirane"

RUN apt-get update
RUN apt-get upgrade
RUN apt-get install -y locales language-pack-en-base
RUN locale-gen $LANG

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections

RUN apt-get install -y dialog apt-utils curl zip unzip nano
RUN apt-get install -y sudo

RUN echo "root:root" | chpasswd
RUN useradd docker && echo "docker:docker" | chpasswd
RUN echo "docker ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN mkdir -p /home/docker && chown -R docker:docker /home/docker && cd /home/docker &&\
    chown -R docker:docker /usr/local/sbin && chown -R docker:docker /usr/local/bin &&\
    mkdir -p /home/docker/.composer && chown -R docker:docker /home/docker/.composer

USER docker

RUN sudo apt-get install -y git
RUN git config --global user.name ${git-user} && git config --global user.email ${git-email}

RUN sudo apt-get install -y software-properties-common iptables
RUN sudo add-apt-repository ppa:ondrej/nginx &&\ 
    sudo apt-get install -y nginx ufw &&\
    sudo ufw allow 'Nginx HTTP' &&\
    sudo service nginx start
RUN sudo add-apt-repository ppa:ondrej/php &&\
    sudo apt-get install -y php7.4 php7.4-bcmath php7.4-mbstring php7.4-curl php7.4-cli php7.4-xml php7.4-soap php7.4-mysql php7.4-zip

COPY ./laravel /etc/nginx/sites-available/laravel

RUN php -r "copy('https://getcomposer.org/installer', '/home/docker/composer-setup.php');" &&\
    php -r "if (hash_file('sha384', '/home/docker/composer-setup.php') === 'a5c698ffe4b8e849a443b120cd5ba38043260d5c4023dbf93e1558871f1f07f58274fc6f4c93bcfd858c6bd0775cd8d1') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" &&\
    php /home/docker/composer-setup.php --install-dir=/usr/local/bin --filename=composer &&\
    php -r "unlink('/home/docker/composer-setup.php');"

RUN composer global require laravel/installer

RUN mkdir -p /home/docker/.nvm && curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.1/install.sh | bash
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION && nvm use --delete-prefix $NODE_VERSION"
