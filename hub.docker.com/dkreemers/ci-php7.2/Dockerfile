FROM php:7.2-cli-stretch

RUN echo "jenkins:x:1000:1000::/var/jenkins_home:/bin/bash" >> /etc/passwd

RUN apt-get update && apt-get install -y \
unzip \
wget \
curl \
git \
subversion \
openssl \
mercurial \
rsync \
zlib1g-dev

RUN pecl install xdebug \
&& docker-php-ext-enable xdebug \
&& docker-php-ext-install zip mysqli

COPY composer-installer.sh /usr/bin/composer-installer
RUN chmod +x /usr/bin/composer-installer && composer-installer
