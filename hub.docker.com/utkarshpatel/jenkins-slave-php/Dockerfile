FROM jenkinsci/jnlp-slave:latest
MAINTAINER Utkarsh Patel <itismeutkarsh@gmail.com>

USER root

RUN printf "\n\n==== Install depedency ====\n" \
 && apt-get update && apt install -y \
  php7.0 \
  php7.0-curl \
  php7.0-json \
  php7.0-cgi \
  php7.0-fpm \
  autoconf \
  automake \
  libxml2-dev \
  libcurl4-openssl-dev \
  libssl-dev \
  openssl \
  gettext \
  libicu-dev \
  libmcrypt-dev \
  libmcrypt4 \
  libbz2-dev \
  libreadline-dev \
  build-essential \
  libmhash-dev \
  libmhash2 \
  libxslt1-dev \
  rsync

RUN printf "\n\n==== Install phpbrew ====\n" \
 && curl -L -O https://github.com/phpbrew/phpbrew/raw/master/phpbrew \
 && chmod +x phpbrew \
 && mv phpbrew /usr/bin \
 && cd /usr/local/include \
 && ln -s /usr/include/x86_64-linux-gnu/curl curl \
 && apt-get install -y libcurl4-gnutls-dev

USER jenkins

RUN printf "\n\n==== Install php 7.2.18 ====\n" \
 && phpbrew init \
 && echo 'source /home/jenkins/.phpbrew/bashrc' >> /home/jenkins/.bashrc \
 && phpbrew install -j $(nproc) 7.2.18 +small +hash -debug -- --with-libdir=lib/x86_64-linux-gnu \
 && export PHPBREW_PHP=php-7.2.18 \
 && phpbrew switch 7.2.18 \
 && phpbrew clean php-7.2.18

USER root
RUN printf "\n\n==== Install composer ====\n" \
  && echo '/home/jenkins/.phpbrew/php/php-7.2.18/bin/php "$@"' > /usr/bin/php \
  && chmod +x /usr/bin/php \
  && curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }" \
  && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer \
  && rm -rf /tmp/composer-setup.php

ENTRYPOINT ["jenkins-slave"]