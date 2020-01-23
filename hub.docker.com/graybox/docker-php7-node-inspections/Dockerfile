FROM alpine:3.9

RUN apk --no-cache upgrade && \
    apk --no-cache add  \
      bash \
      sudo \
      curl \
      grep \
      file \
      wget \
      openssh-client \
      git \
      php7 \
      php7-apache2\
      php7-apcu \
      php7-bcmath \
      php7-ctype \
      php7-curl \
      php7-dom \
      php7-gd \
      php7-iconv \
      php7-imagick \
      php7-intl \
      php7-json \
      php7-mbstring \
      php7-openssl \
      php7-pdo_mysql \
      php7-pdo_pgsql \
      php7-pdo_sqlite \
      php7-phar \
      php7-redis \
      php7-session \
      php7-simplexml \
      php7-tokenizer \
      php7-xdebug \
      php7-xml \
      php7-xmlwriter \
      php7-zip \
      php7-zlib \
      nodejs \
      nodejs-npm \
      apache2 \
      mysql-client \
      jq \
      py2-pip \
      supervisor && \
    rm /var/www/localhost/htdocs/*

RUN npm install -g yarn
RUN pip install awscli

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
RUN mkdir -p /run/apache2 && ln -sf /dev/stdout /var/log/apache2/access.log && ln -sf /dev/stderr /var/log/apache2/error.log

# Inspection tools
RUN mkdir -p /etc/blackfire
RUN mkdir -p /var/run/blackfire
COPY blackfire-agent /etc/blackfire/agent
COPY install_blackfire.sh /usr/local/bin/install_blackfire.sh
COPY supervisord.conf /etc/supervisord.conf
RUN install_blackfire.sh
RUN curl -L https://download.newrelic.com/php_agent/archive/8.2.0.221/newrelic-php5-8.2.0.221-linux-musl.tar.gz | tar -C /tmp -zx && \
    NR_INSTALL_USE_CP_NOT_LN=1 NR_INSTALL_SILENT=1 /tmp/newrelic-php5-*/newrelic-install install && \
      rm -rf /tmp/newrelic-php5-* /tmp/nrinstall*

EXPOSE 80

COPY httpd-foreground.sh /usr/local/bin/

CMD ["httpd-foreground.sh"]
