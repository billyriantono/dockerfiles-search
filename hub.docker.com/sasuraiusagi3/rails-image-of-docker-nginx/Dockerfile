FROM ubuntu:latest
MAINTAINER Takumu Uyama
ARG APP_NAME=rails_app
ARG MODE=development
RUN apt-get update && apt-get -y upgrade && apt-get -y install software-properties-common tzdata && echo 'mysql-server-5.7 mysql-server/root_password password password' | debconf-set-selections && echo 'mysql-server-5.7 mysql-server/root_password_again password password' | debconf-set-selections
RUN apt-get -y install nodejs libcurl4-openssl-dev libapr1-dev libaprutil1-dev libxml2 libxslt-dev libffi-dev build-essential patch libssl-dev mysql-server libmysqlclient-dev git libreadline-dev curl
RUN cd /usr/local && git clone https://github.com/sstephenson/rbenv.git .rbenv && git clone https://github.com/sstephenson/ruby-build.git .rbenv/plugins/ruby-build
ENV RBENV_ROOT=/usr/local/.rbenv PATH="/usr/local/.rbenv/bin:$PATH"
RUN rbenv install 2.4.0 && rbenv global 2.4.0 && rbenv rehash && eval "$(rbenv init -)" && gem install rails passenger --no-document && passenger-install-nginx-module --auto
RUN echo 'export RBENV_ROOT=/usr/local/.rbenv\nexport PATH="/usr/local/.rbenv/bin:$PATH"\neval "$(rbenv init -)"' >> ~/.bashrc
COPY ./$MODE/nginx.conf /opt/nginx/conf
COPY ./my.cnf /etc/mysql
RUN mkdir -p /var/www/html/$APP_NAME && /opt/nginx/sbin/nginx -t
RUN useradd -b /bin/false $APP_NAME
WORKDIR /var/www/html/$APP_NAME
CMD service mysql restart && /opt/nginx/sbin/nginx && tail -f /dev/null
