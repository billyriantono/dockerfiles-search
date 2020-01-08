FROM ubuntu:latest

RUN echo "deb http://ppa.launchpad.net/ondrej/php5-5.6/ubuntu trusty main" >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-key E5267A6C && \
    echo "deb http://ppa.launchpad.net/gluster/glusterfs-3.6/ubuntu trusty main" >> /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-key 3FE869A9  && \
    apt-get update && \
    apt-get install -y glusterfs-client git vim wget curl apache2 \
    php5 php5-mysql php5-mcrypt php5-intl php5-curl php5-imagick php5-memcache php5-gd php5-xsl \
    supervisor rsyslog && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Enable php mcrypt module
RUN php5enmod mcrypt gd opcache

# Enable basic apache mods
RUN a2enmod rewrite headers


