FROM desktophero/chefdk-buildess
MAINTAINER Jason Walker <desktophero@gmail.com>

RUN apt-get install -y \
    mysql-server-5.6 && \
    service mysql stop && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# pre-install some specific Ruby Gems into Chef DK
RUN chef gem install \
  rack-test:0.6.3 \
  ruby-debug-ide:0.6.0 \
  sinatra:1.4.6 \
  thin:1.6.4 \
  require_all:1.3.3 \
  --no-ri --no-rdoc
