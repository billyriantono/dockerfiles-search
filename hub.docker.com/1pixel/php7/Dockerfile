FROM debian:jessie


RUN  apt-get update && apt-get install -y curl wget && \
    echo "export TERM=xterm" >> /root/.bashrc && \
    echo Europe/Paris > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata && \
    echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list.d/dotdeb.org.list && \
    echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list.d/dotdeb.org.list && \
    wget -O- http://www.dotdeb.org/dotdeb.gpg | apt-key add - && \


  apt-get update && \
  apt-get install -y \
  git \
  ssmtp \
  zip \
  apache2 \
  libapache2-mod-php7.0 \
  locales \
  php7.0-fpm \
  php7.0-bcmath \
  php7.0-mysql \
  php7.0-gd \
  php7.0-imagick \
  php7.0-curl \
  php7.0-cli \
  php7.0-zip \
  php7.0-intl \
  php7.0-tidy \
  php7.0-json \
  php7.0-soap \
  php7.0-common \
  php7.0-bz2 \
  php7.0-mcrypt \
  php7.0-common \
  php7.0-xml \ 
  php7.0-apcu php7.0-apcu-bc php7.0-memcached nodejs drush vim \ 
  php7.0-redis \
  && rm -rf /var/lib/apt/lists/*


#Ajout ssmpt
ADD ssmtp.conf /etc/ssmtp/ssmtp.conf
RUN usermod -u 1000 www-data && a2enmod rewrite

