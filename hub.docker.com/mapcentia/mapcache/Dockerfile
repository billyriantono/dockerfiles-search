FROM debian:stretch
MAINTAINER Martin Høgh<mh@mapcentia.com>

RUN  export DEBIAN_FRONTEND=noninteractive
ENV  DEBIAN_FRONTEND noninteractive

# Install packages
RUN apt-get -y update  --fix-missing
RUN apt-get -y install sudo vim wget curl apache2 libfcgi-dev apache2-dev cmake g++ build-essential inotify-hookable \
    libgdal-dev libgdal-dev libgeos-dev libpng-dev libjpeg-dev libcurl4-gnutls-dev libpcre3-dev libpixman-1-dev libsqlite3-dev libtiff5-dev git \
    supervisor libdb5.3 libdb5.3++ libdb5.3++-dev

RUN cd ~ && \
    git clone http://github.com/mapserver/mapcache.git

RUN cd ~ && \
    cd mapcache &&\
    mkdir build &&\
    cd build &&\
    cmake -DWITH_BERKELEY_DB=ON .. &&\
    make &&\
    make install &&\
    ldconfig

# Change default port
RUN sed 's/Listen 80/Listen 5555/' -i /etc/apache2/ports.conf

RUN a2enmod headers
RUN a2dismod -f mime dir auth_basic authn_core access_compat authn_file authz_host authz_user filter deflate authn_file negotiation autoindex reqtimeout setenvif status

# Start httpd with apache2ctl, so the lock file is created
RUN apache2ctl start

# Add apache config file from Docker repo
ADD conf/apache/000-default.conf /etc/apache2/sites-enabled/
ADD conf/apache/mapcache.conf /etc/apache2/sites-enabled/

# Add the watch_mapcache_changes.sh
COPY watch_mapcache_changes.sh /watch_mapcache_changes.sh
RUN chmod +x /watch_mapcache_changes.sh

# Add the reload.js
COPY reload.js /reload.js

RUN curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh &&\
    bash nodesource_setup.sh &&\
    apt-get install -y nodejs

RUN mkdir /mapcache
RUN cp /root/mapcache/mapcache.xml /mapcache/

# Share dirs
VOLUME  ["/var/log", "/etc/apache2", "/mapcache", "/tmp"]

ADD conf/apache/run-apache.sh /
RUN chmod +x /run-apache.sh

# Add Supervisor config and run the deamon
ADD conf/supervisor/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]