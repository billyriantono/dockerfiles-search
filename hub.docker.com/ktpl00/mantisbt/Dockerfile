From ubuntu:16.04

MAINTAINER Yogesh Sharma <yogesh.sharma@krishtechnolabs.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y vim \
    && apt-get install -y software-properties-common \
    && apt-get install -y python-software-properties \
    && apt-get install -y apt-transport-https \
    && apt-get install -y build-essential \
    && apt-get install -y libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev \
    && apt-get install -y tcl8.5 \
    && apt-get install -y wget \
    && apt-get install -y cron \
    && apt-get install -y curl \
    && apt-get install -y rsync \
    && apt-get install -y git \
    && apt-get install -y supervisor \
    && apt-get install -y psmisc \
    && apt-get install -y tree \
    && apt-get install -y rsyslog \ 
    && apt-get install -y lsb \
    && apt-get install -y openssh-server \
    && apt-get install -y sudo \
    && mkdir /var/run/sshd \
    && sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && apt-get install -y language-pack-en-base \
    && apt-get update \
    && locale-gen en_US.UTF-8 \
    && export LANG=en_US.UTF-8 \
    && LC_ALL=en_US.UTF-8 \
    && apt-get update \
    && apt-get install -y python-software-properties \
    && apt-get update \
    && apt-get install -y apache2 \
    && apt-get install -y apache2-utils \
    && apt-get install -y debconf-utils \
    && apt-get update \
    && apt-get install -y mysql-client-5.7 \
    && LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get install -y libapache2-mod-php7.0 \
    && apt-get install -y php7.0-fpm php7.0-mysql \
    && apt-get install -y php7.0-cli php7.0-common php7.0-json php7.0-opcache php7.0-gd php7.0-intl php7.0-gd php7.0-curl \
    && apt-get install -y php7.0-mcrypt php7.0-mbstring php7.0-zip php7.0-xml php7.0-soap php7.0-bcmath php7.0-xmlrpc \
    && apt-get install -y php-mbstring \
    && apt-get install -y php-gettext \
    && mkdir /var/run/php \
    && rm -rf /var/www/html/* \
    && mkdir -pv /webroot \
    && cd /webroot \
    && wget http://excellmedia.dl.sourceforge.net/project/mantisbt/mantis-stable/2.19.0/mantisbt-2.19.0.tar.gz \
    && tar -zxvf mantisbt-2.19.0.tar.gz \
    && mv mantisbt-2.19.0 mantisbt \
    && rm -rf mantisbt-2.19.0.tar.gz \
    && apt-get update \
    && a2enmod rewrite \
    && service apache2 restart

#Configuration-Tools
ADD tools/docker/apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf
ADD tools/docker/apache2/apache2.conf /etc/apache2/apache2.conf
ADD tools/docker/php/apache2/php.ini /etc/php/7.0/apache2/php.ini
ADD tools/docker/php/cli/php.ini /etc/php/7.0/cli/php.ini
ADD tools/docker/supervisor/supervisord.conf /etc/supervisor/supervisord.conf
ADD tools/docker/supervisor/conf.d/apps.conf /etc/supervisor/conf.d/apps.conf
ADD tools/docker/scripts/start.sh /start.sh
ADD tools/docker/scripts/entrypoint.sh /entrypoint.sh

RUN chmod +x /*.sh

EXPOSE 22 80 443 3306

ENTRYPOINT ["/bin/bash", "/entrypoint.sh"]
CMD ["/bin/bash", "/start.sh"]
