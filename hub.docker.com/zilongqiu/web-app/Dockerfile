FROM php:5.6-fpm
MAINTAINER Zi-long QIU <zilong.qiu@gmail.com>

RUN mkdir /home/workspace
WORKDIR /home/workspace

RUN apt-get update && apt-get install -y \
    curl \
    git \
    vim \
    zsh

RUN  php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/local/bin --filename=composer \
    && chmod +x /usr/local/bin/composer

RUN curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | bash
COPY ./configs/zshrc.zsh-template /root/.zshrc
RUN chsh -s `which zsh`
