FROM nextcloud:16.0.1-fpm
RUN set -x; \
 sed -i "s#deb http://deb.debian.org/debian stretch main#deb http://deb.debian.org/debian stretch main non-free#g" /etc/apt/sources.list \
 && sed -i "s#deb http://security.debian.org/debian-security stretch/updates main#deb http://security.debian.org/debian-security stretch/updates main non-free#g" /etc/apt/sources.list \
 && sed -i "s#deb http://deb.debian.org/debian stretch-updates main#deb http://deb.debian.org/debian stretch-updates main non-free#g" /etc/apt/sources.list \
 && apt-get update \
 && apt-get install -y smbclient \
 && apt-get install -y memcached \
 && apt-get install -y libsmbclient-dev \
 && apt-get install -y unrar \
 && apt-get install -y p7zip p7zip-full \
 && rm -rf /var/lib/apt/list/* \
 && rm -rf /var/cache/apt/archives/*
RUN pecl install -o -f smbclient \
 && docker-php-ext-enable smbclient \
 && rm -rf /tmp/pear
