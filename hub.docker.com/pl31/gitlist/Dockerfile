FROM pl31/debian:jessie
MAINTAINER Patrick Büch <dh@paco.pl31.de>

# install apache2 + php
RUN echo "Europe/Berlin" > /etc/timezone && \
    dpkg-reconfigure tzdata && \
    apt-get -y update && \
    apt-get -y upgrade && \
    apt-get -y install \
        apache2 \
        libapache2-mod-php5

COPY files/ /

# install gitlist
RUN (cd /var/www/html/ && \
    curl -0 https://s3.amazonaws.com/gitlist/gitlist-master.tar.gz | tar -zx) && \
    (cd /var/www/html/gitlist/ && \    
    mv config.ini-example config.ini && \
    mkdir cache && chmod a+rwx cache/) && \
    (cd /home/ && \
    mkdir -p /home/git/repositories/) && \
    a2enmod rewrite && \
    ln -s /etc/apache2/conf-available/gitlist.conf /etc/apache2/conf-enabled/gitlist.conf

# repositories folder
VOLUME /home/git/repositories/
# web server port
EXPOSE 80

CMD service apache2 start && while true; do sleep 1d; done
