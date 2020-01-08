########################################################################################################################
## PHP
## use offical image as base
FROM debian:stretch

# Install dependencies
RUN sed -i "s/httpredir.debian.org/mirror.unitedcolo.de/" /etc/apt/sources.list \
    && apt-get update \
    && apt-get -y install apache2 wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

RUN a2dissite 000-default \
    && /usr/sbin/a2enmod ssl proxy proxy_http proxy_fcgi rewrite headers deflate expires

########################################################################################################################
ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
        && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
        && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && \
    chmod +x /usr/local/bin/* && \
    mkdir -p /etc/dockerize/templates && \
    sed -ri ' \
      s!^(\s*CustomLog)\s+\S+!\1 /proc/self/fd/1!g; \
      s!^(\s*RewriteLog)\s+\S+!\1 /proc/self/fd/1!g; \
      s!^(\s*ErrorLog)\s+\S+!\1 /proc/self/fd/2!g; \
    ' /etc/apache2/conf-available/* /etc/apache2/sites-available/*

COPY virtualhost.conf.tpl /etc/dockerize/templates/virtualhost.conf.tpl

VOLUME /var/www/html

ENTRYPOINT ["dockerize", "-template", "/etc/dockerize/templates/virtualhost.conf.tpl:/etc/apache2/sites-enabled/virtualhost.conf"]
CMD usermod -u $DOCKER_USER_ID www-data && /usr/sbin/apache2ctl -D FOREGROUND