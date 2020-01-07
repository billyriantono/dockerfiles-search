FROM debian:stretch-slim
MAINTAINER Mike Bruder

# Variables
ARG VERSION="latest"
ARG WEB_ROOT="htdocs"
ENV GROUP="youtube-dl"
ENV USER="youtube-dl"
ENV php_ini /etc/php/7.0/fpm/php.ini
ENV fpm_conf /etc/php/7.0/fpm/php-fpm.conf
ENV fpm_pool /etc/php/7.0/fpm/pool.d/www.conf
ENV nginx_conf /etc/nginx/nginx.conf

RUN apt-get update -qq && apt-get install -qqy gnupg2 curl

RUN curl -O http://www.dotdeb.org/dotdeb.gpg \
   && apt-key add dotdeb.gpg \
   && rm -rf dotdeb.gpg
RUN echo "deb http://packages.dotdeb.org stretch all" >> /etc/apt/sources.list \
   && echo "deb-src http://packages.dotdeb.org stretch all" >> /etc/apt/sources.list

# Install Packages
RUN apt-get update -qq \
    && apt-get install --no-install-recommends --no-install-suggests -qqy \ 
    nano sed make ffmpeg rtmpdump tar ssl-cert supervisor nginx-extras php7.0-dev php7.0-fpm php-pear procps

# Install PHP Extensions
RUN pecl install inotify

# Hacking configs
RUN echo "Hacking configs" \
    && sed -i 's/max_execution_time = 30/max_execution_time = 240/g' ${php_ini} \
    && sed -i 's/display_errors = Off/display_errors = On/g' ${php_ini} \
	&& sed -i "s/post_max_size\s*=\s*8M/post_max_size = 100M/g" ${php_ini} \
    && sed -i 's/memory_limit = 128M/memory_limit = 256M/g' ${php_ini} \
    && echo "extension=inotify.so" >> ${php_ini} \
	&& sed -i "s/;daemonize\s*=\s*yes/daemonize = no/g" ${fpm_conf} \
    && sed -i 's/listen = \/run\/php\/php7.0-fpm.sock/listen = \/var\/run\/php-fpm.sock/g' ${fpm_pool} \
    && sed -i 's/access_log \/var\/log\/nginx\/access.log;/access_log \/proc\/self\/fd\/2 combined;/g' ${nginx_conf} \
    && sed -i 's/error_log \/var\/log\/nginx\/error.log;/error_log \/proc\/self\/fd\/2 error;/g' ${nginx_conf} \
    && echo "daemon off;" >> ${nginx_conf}

# Install youtube-dl Package
RUN echo "Install youtube-dl" \
    && curl -L https://yt-dl.org/downloads/${VERSION}/youtube-dl -o /usr/local/bin/youtube-dl \
    && chmod 755 /usr/local/bin/youtube-dl

# Clean up 
RUN echo "Clean up" \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && rm -rf /etc/nginx/conf.d/* /usr/share/nginx/html/* /var/www/html/

# Setup structure
RUN mkdir -p /var/www/${WEB_ROOT} \
    && mkdir -p /var/www/${WEB_ROOT}/media \
    && mkdir -p /var/www/${WEB_ROOT}/tmp \
    && adduser --home /var/www/${WEB_ROOT} --shell /bin/bash --disabled-password --gecos "${USER}" ${USER} \
    && chown -R ${USER}:${GROUP} /var/www/${WEB_ROOT} /var/lib/nginx /tmp

# Copy files
COPY supervisord.conf /etc/supervisor/supervisord.conf
COPY ./start.sh /start.sh
RUN chmod +x start.sh

ENTRYPOINT ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisor/supervisord.conf"]

EXPOSE 80 443