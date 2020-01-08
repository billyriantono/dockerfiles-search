FROM phusion/baseimage:0.9.16
MAINTAINER virtike <virtike@github>

# Set correct environment variables
ENV HOME /root
ENV HTTPD_USER www-data
ENV DEBIAN_FRONTEND noninteractive
ENV LC_ALL C.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

# Use baseimage-docker's init system
CMD ["/sbin/my_init"]

# Configure user nobody to match unRAID's settings
RUN \
  usermod -u 99 nobody && \
  usermod -g 100 nobody && \
  usermod -d /home nobody && \
  chown -R nobody:users /home

# Disable SSH
RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

# install h5ai and patch configuration
RUN \
  add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ trusty universe multiverse" && \
  add-apt-repository "deb http://us.archive.ubuntu.com/ubuntu/ trusty-updates universe multiverse" && \
  apt-get update -q && \
  apt-get install -qy nginx php5-fpm wget unzip patch && \
  apt-get install -qy libav-tools imagemagick graphicsmagick zip php5-gd &&\
  apt-get clean -y && \
  rm -rf /var/lib/apt/lists/* && \
  wget https://release.larsjung.de/h5ai/h5ai-0.29.2.zip && \
  unzip h5ai-0.29.2.zip -d /usr/share/h5ai

# patch h5ai because we want to deploy it ouside of the document root and use /var/www as root for browsing
COPY class-setup.php.patch class-setup.php.patch
RUN patch -p1 -u -d /usr/share/h5ai/_h5ai/private/php/core/ -i /class-setup.php.patch && rm class-setup.php.patch

# set up config redirect
RUN cp /usr/share/h5ai/_h5ai/private/conf/options.json /usr/share/h5ai/_h5ai/private/conf/options.json.bak
RUN rm /usr/share/h5ai/_h5ai/private/conf/options.json
RUN ln -s /config/options.json /usr/share/h5ai/_h5ai/private/conf/options.json

RUN cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
RUN rm /etc/nginx/nginx.conf
RUN ln -s /config/nginx/nginx.conf /etc/nginx/nginx.conf

# make the cache writable
RUN chown ${HTTPD_USER} /usr/share/h5ai/_h5ai/public/cache/
RUN chown ${HTTPD_USER} /usr/share/h5ai/_h5ai/private/cache/

# add h5ai as the only nginx site
ADD h5ai.nginx.conf /etc/nginx/sites-available/h5ai
RUN ln -s /etc/nginx/sites-available/h5ai /etc/nginx/sites-enabled/h5ai
RUN rm /etc/nginx/sites-enabled/default

WORKDIR /var/www

# expose only nginx HTTP port
EXPOSE 80

# Expose Volumes
VOLUME ["/var/www", "/config", "/log"]

# Add firstrun.sh to execute during container startup
ADD firstrun.sh /etc/my_init.d/firstrun.sh
RUN chmod +x /etc/my_init.d/firstrun.sh

# Add h5ai to runit
RUN mkdir /etc/service/h5ai
ADD h5ai.sh /etc/service/h5ai/run
RUN chmod +x /etc/service/h5ai/run
