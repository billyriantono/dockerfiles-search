# Dockerizing nginx-RTMP: Dockerfile for building nginx-RTMP images
# Based on ubuntu:latest, installs nginx-RTMP

# Format: FROM    repository[:version]
FROM       ubuntu:latest

# Format: MAINTAINER Name <email@addr.ess>
MAINTAINER Andreas W. Prang <writeAmail@me.com>

# VARIABLES
# ENV nginxVersion nginx-1.9.2
ENV nginxVersion nginx-1.11.3

# Installation:
RUN apt-get update;\
        apt-get -y install wget;\
        apt-get -y install unzip;\
        apt-get install -y build-essential libpcre3 libpcre3-dev libssl-dev

# Install nginx with RTMP
RUN mkdir /tmp/working && cd /tmp/working;\
        wget http://nginx.org/download/${nginxVersion}.tar.gz;\
        wget https://github.com/arut/nginx-rtmp-module/archive/master.zip;\
        tar -zxvf ${nginxVersion}.tar.gz;\
        unzip master.zip;\
        cd ${nginxVersion};\
        ./configure --with-http_ssl_module --with-http_v2_module --add-module=../nginx-rtmp-module-master;\
        make install clean

RUN rm -r /tmp/working

# Install Let's Encrypt
RUN apt-get -y install git bc;
RUN git clone https://github.com/letsencrypt/letsencrypt /opt/letsencrypt;

# ADD nginx_sites-available_default /etc/nginx/sites-available/default

RUN openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048

# Install daemon
RUN wget https://raw.github.com/JasonGiedymin/nginx-init-ubuntu/master/nginx -O /etc/init.d/nginx;\
        chmod +x /etc/init.d/nginx;\
        update-rc.d nginx defaults

# Install additional decoder
RUN apt-get install -y ffmpeg;

ADD nginx.conf /usr/local/nginx/conf/nginx.conf.new
RUN rm /usr/local/nginx/conf/mime.types
ADD mime.types /usr/local/nginx/conf/mime.types

RUN mkdir -p /var/log/nginx/
RUN ln -s /usr/local/nginx/html /var/www
RUN mkdir -p /var/www/HLS/
ADD stat.xsl /var/www/HLS/stat.xsl
ADD html/* /var/www/

# expose HTTP
EXPOSE 80
EXPOSE 443
EXPOSE 1935

# Pre-Install dependencies to run letsencrypt-auto
RUN apt-get install -y augeas-lenses dh-python dialog libaugeas0 libexpat1-dev libffi-dev libmpdec2 libpython-dev libpython-stdlib libpython2.7 libpython2.7-dev libpython2.7-minimal libpython2.7-stdlib libpython3-stdlib libpython3.5-minimal libpython3.5-stdlib mime-support python python-dev python-minimal python-pip-whl python-pkg-resources python-virtualenv python2.7 python2.7-dev python2.7-minimal python3 python3-minimal python3-pkg-resources python3-virtualenv python3.5 python3.5-minimal virtualenv

ADD postInstall.sh postInstall.sh
RUN chmod +x postInstall.sh
## run as daemon

# CMD /opt/letsencrypt/letsencrypt-auto certonly --agree-tos --text --non-interactive --register-unsafely-without-email -a webroot --webroot-path=/var/www/ -d stream.demokratielive.org; service nginx start
# CMD /opt/letsencrypt/letsencrypt-auto renew; service nginx start
CMD ./postInstall.sh


## run interactive
# CMD service nginx start & /bin/bash
# CMD /bin/bash


# Clean // TODO: NOT WORKING
# RUN apt-get -y purge wget unzip build-essential libpcre3 libpcre3-dev libssl-dev software-properties-common
