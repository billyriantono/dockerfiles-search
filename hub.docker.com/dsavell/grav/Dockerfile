FROM bitnami/minideb:stretch

RUN \
  ## Install Pre-reqs
  install_packages \
    apt-transport-https \
    ca-certificates \
    curl \
    lsb-release \
    nginx \
    unzip \
    wget && \
  ## Install PHP APT Repository
  wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
  echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php7.3.list && \
  ## Install PHP 7.3
  install_packages \
    php7.3 \
    php7.3-fpm \
    php7.3-gd \
    php7.3-curl \
    php7.3-zip \
    php7.3-mbstring \
    php7.3-xml && \
  ## Install GRAV
  rm -rf /var/www/* && \
  GRAV_VERSION=$(curl -sX GET "https://api.github.com/repos/getgrav/grav/releases/latest" | awk '/tag_name/{print $4;exit}' FS='[""]') && \
  curl -o grav-v${GRAV_VERSION}.zip -L https://github.com/getgrav/grav/releases/download/${GRAV_VERSION}/grav-v${GRAV_VERSION}.zip && \
  unzip grav-v${GRAV_VERSION}.zip -d /var/www && \
  rm -rf grav-v${GRAV_VERSION}.zip && \
  cp -R /var/www/grav/* /var/www && \
  rm -rf /var/www/grav && \
  ## Set Correct GRAV Permissions
  chgrp -R www-data /var/www && \
  find /var/www -type f | xargs chmod 664 && \
  find /var/www/bin -type f | xargs chmod 775 && \
  find /var/www -type d | xargs chmod 775 && \
  find /var/www -type d | xargs chmod +s && \
  umask 0002 && \
  ## Nginx Logs
  ln -sf /dev/stdout /var/log/nginx/access.log && \
  ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

COPY root/ /

CMD ["/init"]
