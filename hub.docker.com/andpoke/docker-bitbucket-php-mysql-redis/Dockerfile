FROM debian:stretch-slim
MAINTAINER Andy Van Trout <andreiv@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL en_US.UTF-8
ENV LANGUAGE en_US:en
ENV REDIS_VERSION 3.2.8
ENV REDIS_DOWNLOAD_URL http://download.redis.io/releases/redis-3.2.8.tar.gz
ENV REDIS_DOWNLOAD_SHA1 6780d1abb66f33a97aad0edbe020403d0a15b67f



RUN groupadd -r redis && useradd -r -g redis redis

RUN set -ex \
	\
	&& buildDeps=' \
		gcc \
		libc6-dev \
		make \
		wget \
	' \
	&& apt-get update \
	&& apt-get install -y $buildDeps --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/* \
	&& wget -O redis.tar.gz "$REDIS_DOWNLOAD_URL" \
	&& echo "$REDIS_DOWNLOAD_SHA1 *redis.tar.gz" | sha1sum -c - \
	&& mkdir -p /usr/src/redis \
	&& tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 \
	&& rm redis.tar.gz \
	&& make -C /usr/src/redis \
	&& make -C /usr/src/redis install \
	&& rm -r /usr/src/redis

RUN mkdir /data && chown redis:redis /data

RUN \
 apt-get update &&\
 apt-get -y --no-install-recommends install locales apt-utils wget ca-certificates apt-transport-https lsb-release gnupg &&\
 echo "deb http://repo.mysql.com/apt/debian/ stretch mysql-5.7\ndeb-src http://repo.mysql.com/apt/debian/ stretch mysql-5.7" > /etc/apt/sources.list.d/mysql.list &&\

wget -q https://packages.sury.org/php/apt.gpg -O- | apt-key add - &&\
echo "deb https://packages.sury.org/php/ stretch main" | tee /etc/apt/sources.list.d/php.list &&\

 wget -O /tmp/RPM-GPG-KEY-mysql https://repo.mysql.com/RPM-GPG-KEY-mysql &&\
 apt-key add /tmp/RPM-GPG-KEY-mysql &&\
 apt-get update &&\
 echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen &&\
 locale-gen en_US.UTF-8 &&\
 /usr/sbin/update-locale LANG=en_US.UTF-8 &&\
 echo "mysql-server mysql-server/root_password password root" | debconf-set-selections &&\
 echo "mysql-server mysql-server/root_password_again password root" | debconf-set-selections &&\
 apt-get -y --no-install-recommends install gnupg git subversion php7.2-apcu php7.2-bcmath php7.2-cli php7.2-curl php7.2-gd php7.2-geoip php7.2-gettext libxml2-dev php7.2-soap php7.2-imagick php7.2-intl php7.2-json php7.2-mbstring php7.2-xml php7.2-mysql php7.2-xdebug php7.2-xmlrpc php7.2-zip php7.2-dev pkg-config imagemagick openssh-client curl software-properties-common gettext zip mysql-client mysql-server ruby python python3 perl php-pear php7.2-common php7.2-opcache php7.2-memcached memcached &&\


 curl -sSL https://deb.nodesource.com/setup_6.x | bash - &&\
 apt-get -y --no-install-recommends install nodejs &&\
 apt-get autoclean && apt-get clean && apt-get autoremove

RUN \
 sed -ri -e "s/^variables_order.*/variables_order=\"EGPCS\"/g" /etc/php/7.2/cli/php.ini &&\
 echo "xdebug.max_nesting_level=250" >> /etc/php/7.2/mods-available/xdebug.ini

 # Install the mongodb extension
RUN \
 apt-get update \
 && apt-get install -y --no-install-recommends \
 mongodb \
 gcc \
 make \
 build-essential \
 && pecl install mongodb-1.5.1 \
 && echo "extension=mongodb.so" > /etc/php/7.2/mods-available/ext-mongodb.ini \
 && echo "extension=mongodb.so" > /etc/php/7.2/cli/conf.d/ext-mongodb.ini

RUN \
 curl -sSL https://getcomposer.org/installer | php -- --filename=composer --install-dir=/usr/bin &&\
 curl -sSL https://phar.phpunit.de/phpunit.phar -o /usr/bin/phpunit  && chmod +x /usr/bin/phpunit  &&\
 curl -sSL http://codeception.com/codecept.phar -o /usr/bin/codecept && chmod +x /usr/bin/codecept &&\
 npm install --no-color --production --global gulp-cli webpack mocha grunt &&\
 rm -rf /root/.npm /root/.composer /tmp/* /var/lib/apt/lists/*

