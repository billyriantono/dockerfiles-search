FROM ubuntu:trusty

WORKDIR /var/www/html

EXPOSE 80 443

RUN mkdir -p /var/cache/nginx/proxy_cache && mkdir -p /var/cache/nginx/fastcgi_cache && apt-get update && apt-get -y install \
   debian-archive-keyring curl && rm -rf /var/lib/apt/lists/* && apt-get clean


RUN apt-key adv --recv-keys --keyserver keyserver.ubuntu.com C300EE8C && \
apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449 && \
echo "deb http://ppa.launchpad.net/nginx/stable/ubuntu trusty main" >> /etc/apt/sources.list && \
echo "deb http://dl.hhvm.com/ubuntu trusty-lts-3.15 main" >> /etc/apt/sources.list

RUN apt-get update && apt-get -y install nginx hhvm && rm -rf /var/lib/apt/lists/* && apt-get clean
