FROM ubuntu:latest

MAINTAINER Philipz <philipzheng@gmail.com>

RUN apt-get update && apt-get install -y curl wget build-essential software-properties-common supervisor

# install the nginx/stable repo
RUN add-apt-repository -y ppa:nginx/stable

# install HHVM repo
RUN wget -O - http://dl.hhvm.com/conf/hhvm.gpg.key | sudo apt-key add -
RUN echo deb http://dl.hhvm.com/ubuntu trusty main | sudo tee /etc/apt/sources.list.d/hhvm.list

# update sources and install nginx / HHVM
RUN apt-get update
RUN apt-get install -y nginx hhvm

# stop and disable the services - supervisor runs them
RUN service hhvm stop
RUN service nginx stop
RUN update-rc.d -f nginx remove
RUN update-rc.d -f hhvm remove

# link HHVM to the php-cli
RUN /usr/bin/update-alternatives --install /usr/bin/php php /usr/bin/hhvm 60

# install composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

# configure HHVM
COPY hhvm.conf /etc/nginx/

# disable nginx default site
RUN unlink /etc/nginx/sites-enabled/default
COPY web.conf /etc/nginx/sites-available/web.conf
RUN ln -s /etc/nginx/sites-available/web.conf /etc/nginx/sites-enabled/web.conf
COPY supervisord.conf /etc/supervisor/conf.d/

# expose port 80
EXPOSE 80

# Default Run
CMD ["/usr/bin/supervisord"]
