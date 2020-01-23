FROM ubuntu:16.04

ENV LANG=en_US.UTF-8 LANGUAGE=en_US.UTF-8 LC_ALL=en_US.UTF-8
ENV TZ=Asia/Jakarta FQDN=localhost LARAVEL_ROOT="/var/www/html"

# general
RUN apt-get update && apt-get -y upgrade && \
    apt-get -y install software-properties-common \
    python-software-properties \
    sudo \
    git \
    curl \
    nano \
    wget \
    net-tools \
    locales \
    htop \
    gettext-base \
    iputils-ping && \
    locale-gen en_US.UTF-8

# set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
    apt-get install -y tzdata && \
    dpkg-reconfigure --frontend noninteractive tzdata

# nginx
RUN add-apt-repository -y ppa:nginx/stable && \
    apt-get update && \
    apt-get install -y nginx
ADD etc/nginx/nginx.conf /etc/nginx/nginx.conf
ADD etc/nginx/sites-enabled/default /etc/nginx/sites-available/default

#certbot
RUN add-apt-repository -y ppa:certbot/certbot && \
    apt-get update && \
    apt-get install -y python-certbot-nginx

# create docker group and users
RUN groupadd -r -g 1001 appuser && \
    useradd -rm -d /home/appuser -s /bin/bash -G sudo -u 1001 -g 1001 appuser && \
    echo "appuser:appuser" | chpasswd && \
    echo "appuser ALL=(ALL) NOPASSWD: /usr/bin/certbot" >> /etc/sudoers && \
    echo "appuser ALL=(ALL) NOPASSWD: /usr/sbin/service" >> /etc/sudoers && \
    chown -R appuser:appuser /etc/nginx /var/log/nginx /var/lib/nginx /var/run/ /var/www/html

# add entrypoint
ADD entrypoint.sh /usr/local/bin/docker-entrypoint.sh
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

USER appuser
WORKDIR /home/appuser

EXPOSE 80/tcp 443/tcp
ENTRYPOINT [ "docker-entrypoint.sh" ]
