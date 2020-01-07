FROM node:stretch

LABEL maintainer Alipeng <lipeng.yang@mobvista.com>


RUN set -ex; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		vim \
		apt-transport-https \
		ca-certificates \
		wget && \
	wget -O /etc/apt/trusted.gpg.d/php.gpg https://mirror.xtom.com.hk/sury/php/apt.gpg && \
	echo "deb https://mirror.xtom.com.hk/sury/php/ stretch main" > /etc/apt/sources.list.d/php.list && \
	apt update; \
	apt install -y \
		php7.2-cli \
		php7.2-mysql \
		php7.2-curl \
		php7.2-gd \
		php7.2-mbstring \
		php7.2-xml \
		php7.2-xmlrpc \
		php7.2-zip \
		php7.2-mongodb \
		php7.2-opcache && \
	rm -rf /var/lib/apt/lists/* && \
	npm install -g pm2 && \
	usermod -u 82 www-data &&\
	groupmod -g 83 www-data

# Application environment
WORKDIR /var/www
