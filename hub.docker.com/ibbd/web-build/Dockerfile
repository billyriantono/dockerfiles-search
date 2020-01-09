#
# web开发构建镜像 Dockerfile
# 主要满足laravel5.1, Flarum等的基本要求
#
# https://github.com/ibbd/dockerfile-web-build
#
# sudo docker build -t ibbd/web-build ./
#

# Pull base image.
FROM php:5.6-cli

MAINTAINER Alex Cai "cyy0523xc@gmail.com"

# sources.list
# git clone git@github.com:IBBD/docker-compose.git
# 如果导致apt-get Install不成功，可以先注释这句
ADD sources.list   /etc/apt/sources.list

# ap-get install
RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        libmcrypt-dev \
        libssl-dev \
        nodejs \
        npm \
        git-core \
        vim-tiny \
        zip unzip \
    && apt-get autoremove \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*


# install php modules
# composer 
# composer中国镜像
RUN \
    docker-php-ext-install iconv mcrypt pdo pdo_mysql tokenizer mbstring zip mysqli \
    && cd / \
    && curl -sS https://getcomposer.org/installer -o /composer.php \
    && php composer.php \
    && mv composer.phar /usr/local/bin/composer \
    && rm -f composer.php \
    && chmod 755 /usr/local/bin/composer \
    && composer config -g repositories.packagist composer http://packagist.phpcomposer.com 

# install gulp webpack
RUN \
    npm config set strict-ssl false \
    && npm config set registry "http://registry.npmjs.org/" \
    && npm install -g \
        gulp \
        webpack


# 解决时区问题
ENV TZ "Asia/Shanghai"

# 终端设置
# 执行php-fpm时，默认值是dumb，这时在终端操作时可能会出现：terminal is not fully functional
ENV TERM xterm

# 工作目录
WORKDIR /var/www 


