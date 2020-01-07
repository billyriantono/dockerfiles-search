FROM samtayuk/nginx:1.9
MAINTAINER Samuel Taylor "samtaylor.uk@gmail.com"

# Install php7
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E5267A6C \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu trusty main" >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y -q --no-install-recommends \ 
      cron \
      php7.0-curl \
      php7.0-fpm \
      php7.0-gd \
      php7.0-bz2 \
      php7.0-mysql \
      php7.0-mcrypt \
      php7.0-sqlite \
      php7.0-odbc \
      php7.0-opcache \
      php7.0-pgsql  \
      php-apcu \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /run/php \
    && sed -i '/^;clear_env = no/s/^;//' /etc/php/7.0/fpm/pool.d/www.conf

# Install Forego
RUN wget -P /usr/local/bin https://godist.herokuapp.com/projects/ddollar/forego/releases/current/linux-amd64/forego \
  && chmod u+x /usr/local/bin/forego

COPY Procfile /app/
WORKDIR /app/

COPY index.php /app/www/
COPY default.conf /etc/nginx/conf.d/
COPY php.ini /etc/php/7.0/fpm/conf.d/40-custom.ini

CMD ["/usr/local/bin/forego", "start", "-r"]
