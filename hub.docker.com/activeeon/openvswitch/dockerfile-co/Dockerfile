FROM abegodong/a-s6:3.2
MAINTAINER Abraham Godong <a@rc.lc>

VOLUME ["/contents"]

ENV ENV DEVELOPMENT

# Install PHP-FPM and other dependency packages
RUN apk add -U php php-fpm php-json php-ctype php-curl php-openssl php-mysql ca-certificates openssh-client git && rm -rf /var/cache/apk/*

# Install Caddy
RUN cd /root \
&& curl -sLO https://github.com/mholt/caddy/releases/download/v0.7.0/caddy_linux_amd64.zip \
&& unzip caddy_linux_amd64.zip \
&& mv caddy /usr/bin/caddy \
&& chmod 755 /usr/bin/caddy \
&& rm -rf *

# Install Wordpress
ADD http://wordpress.org/latest.tar.gz /data/src/latest.tar.gz
RUN cd /data/src && tar zxf latest.tar.gz \
&& rm -f latest.tar.gz \
&& mv /data/src/wordpress /data/src/html \
&& mv /data/src/html/wp-content /contents

# Add in all configs
ADD config/Caddyfile /etc/Caddyfile
ADD config/php-fpm.conf /etc/php/php-fpm.conf
ADD service/caddy/run /etc/service/caddy/run
ADD service/php-fpm/run /etc/service/php-fpm/run
RUN chmod +x /etc/service/caddy/run \
&& chmod +x /etc/service/php-fpm/run

EXPOSE 80
