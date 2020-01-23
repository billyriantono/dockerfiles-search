FROM ruby:2.0
MAINTAINER Venka Ashtakala "vashtakala@barquin.com"

EXPOSE 80

#Package installations
RUN apt-get update -y
RUN apt-get install -y vim sudo

RUN curl -sL https://deb.nodesource.com/setup_0.12 | bash -
RUN apt-get install -y nodejs
 
#Add rails user
RUN echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
RUN useradd -g sudo -ms /bin/bash rails

#Fix hostsfile so that sudo doesn't give a warning
RUN echo "127.0.0.1 $(hostname)" >> /etc/hosts

#install basic gems and setup passenger
RUN gem install rails
RUN gem install passenger -v=5.0.11
RUN $GEM_HOME/gems/passenger*/bin/passenger-install-nginx-module
 
#create dir for default webapp
USER rails
RUN /bin/sh -c "cd ~; mkdir webapp"

#finalize nginx setup
USER root
#RUN rm /etc/nginx/sites-available/default
ADD config/docker/nginx/opt/nginx/conf/nginx.conf /opt/nginx/conf/nginx.conf
ADD config/docker/nginx/etc/init.d/nginx /etc/init.d/nginx

# Clean up APT when done.
CMD apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Start Nginx / Passenger
# RUN rm -f /etc/service/nginx/down
# CMD ["service","nginx","start"]


