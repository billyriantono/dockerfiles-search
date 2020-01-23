FROM php:7.2-fpm-stretch

RUN apt-get update && apt-get install -y \
  cron \
  default-mysql-client \
  git \
  gzip \
  libfreetype6-dev \
  libicu-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  libpng-dev \
  libxslt1-dev \
  lsof \
  vim \
  zip

RUN rm -rf /var/lib/apt/lists/*

RUN apt-get update \
  && apt-get install -y \
      procps \
      python \
      python-dev \
      python-pip \
      python-setuptools \
  && pip install --upgrade awscli \
  && apt-get clean

RUN printf "deb http://deb.debian.org/debian stretch-backports main non-free\ndeb-src http://deb.debian.org/debian stretch-backports main non-free" > /etc/apt/sources.list.d/backports.list \
  && apt-get update \
  && apt-get -t stretch-backports install -y libsodium-dev

RUN docker-php-ext-configure \
  gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install \
  bcmath \
  gd \
  intl \
  mbstring \
  opcache \
  pdo_mysql \
  soap \
  sockets \
  sodium \
  xsl \
  zip

RUN groupadd -g 1000 app \
 && useradd -g 1000 -u 1000 -d /var/www -s /bin/bash app

RUN printf '* *\t* * *\tapp\t%s/usr/local/bin/php /var/www/html/update/cron.php\n' >> /etc/crontab
RUN printf '* *\t* * *\tapp\t%s/usr/local/bin/php /var/www/html/bin/magento cron:run\n' >> /etc/crontab
RUN printf '* *\t* * *\tapp\t%s/usr/local/bin/php /var/www/html/bin/magento setup:cron:run\n' >> /etc/crontab

COPY conf/www.conf /usr/local/etc/php-fpm.d/
COPY conf/php.ini /usr/local/etc/php/
COPY conf/php-fpm.conf /usr/local/etc/
COPY bin/cronstart /usr/local/bin/

COPY cert/fisheye.crt /usr/local/share/ca-certificates/
RUN update-ca-certificates

RUN mkdir -p /etc/nginx/html /var/www/html /sock
RUN chown -R app:app /etc/nginx /var/www /usr/local/etc/php/conf.d /sock

USER app:app

VOLUME /var/www

WORKDIR /var/www/html

EXPOSE 9001
