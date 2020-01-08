# NAME: Jenkins 2.107.3
#
# DESCRIPTION: Jenkins image.
#
# REQUIRED ENVS:
# DATA_DIRECTORY (ie. "/home/jenkins/data/")
#
# OPTIONAL ENVS:
# GIT_USER_NAME: (ie. "TDS Servers")
# GIT_USER_EMAIL: (ie. "github@tdsservers.com")
# REDIS_HOST (ie. 127.0.0.1)
# REDIS_PORT (ie. 6379)
# REDIS_DATABASE (ie. 0)
# REDIS_NAMESPACE (ie. "tds", : not allowed)
# REDIS_PASSWORD: (ie. "abcdabcd1234")
# SSH_KEY: (ie. "/home/jenkins/.ssh/id_rsa")
# SSH_PUB_KEY: (ie. "/home/jenkins/.ssh/id_rsa.pub")
#
# OTHER:
# mount the docker.sock from the host into this container for jenkins to be able to run docker commands, ie.
# -v /var/run/docker.sock:/var/run/docker.sock.
#
# The REDIS_ variables are needed for the deploy.sh script to communicate with redis and captain.

FROM thedutchselection/java:8
MAINTAINER Ilja Krijger <ilja@quittheprogram.org>

RUN \
  groupadd --gid 900 --system docker && \
  useradd -g docker -m -u 900 docker

RUN \
  apt-get update && \
  apt-get install -yq apt-transport-https && \
  echo "deb http://http.debian.net/debian jessie-backports main" > /etc/apt/sources.list.d/backports.list && \
  apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D && \
  echo "deb https://apt.dockerproject.org/repo debian-jessie main" > /etc/apt/sources.list.d/docker.list && \
  apt-get update && \
  apt-get install -yq curl && \
  apt-get install -yq redis-tools && \
  apt-get install -yq docker-engine=1.10.3-0~jessie && \
  apt-get install -yq zlib1g-dev && \
  apt-get install -yq libssl-dev && \
  apt-get install -yq libreadline6-dev && \
  apt-get install -yq libyaml-dev && \
  apt-get install -yq libffi-dev && \
  apt-get install -yq libmysqlclient-dev && \
  apt-get install -yq libsqlite3-dev && \
  apt-get install -yq sqlite3 && \
  apt-get install -yq libfreetype6 && \
  apt-get install -yq libfontconfig1 && \
  apt-get install -yq libjpeg-dev && \
  apt-get install -yq libcurl4-openssl-dev && \
  apt-get install -yq libxml2-dev && \
  apt-get install -yq libxslt1-dev && \
  apt-get install -yq qt5-default && \
  apt-get install -yq libqt5webkit5-dev && \
  apt-get install -yq imagemagick && \
  apt-get install -yq mariadb-client && \
  apt-get install -yq xfonts-base && \
  apt-get install -yq xfonts-75dpi && \
  apt-get install -yq xvfb && \
  apt-get install -yq chromedriver && \
  curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
  apt-get install -yq nodejs && \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
  apt-get update && \
  apt-get install -yq yarn && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
  #Always be bashing...
  ln -snf /bin/bash /bin/sh

COPY files/scripts/chruby.sh /etc/profile.d/chruby.sh
COPY files/scripts /usr/local/bin

WORKDIR /tmp

RUN \
  mkdir -p /opt/jenkins && \
  curl -sL -o /opt/jenkins/jenkins.war http://mirrors.jenkins-ci.org/war-stable/2.107.3/jenkins.war

RUN \
  curl -sL -o /tmp/chruby-0.3.9.tar.gz https://github.com/postmodern/chruby/archive/v0.3.9.tar.gz && \
  tar -xzvf chruby-0.3.9.tar.gz && \
  cd chruby-0.3.9/ && \
  make install && \
  cd /tmp && \
  rm -rf chruby-0.3.9 && \
  rm -f chruby-0.3.9.tar.gz

RUN \
  curl -sL -o /tmp/phantomjs-2.1.1-linux-x86_64.tar.bz2 https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
  tar -xvjf phantomjs-2.1.1-linux-x86_64.tar.bz2 --directory /usr/local/share && \
  rm phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
  ln -s /usr/local/share/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin/phantomjs && \
  ln -s /usr/local/share/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/bin/phantomjs

RUN \
  curl -sL -o /tmp/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz && \
  tar -xJf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz && \
  mv wkhtmltox/bin/* /usr/local/bin && \
  rm wkhtmltox-0.12.4_linux-generic-amd64.tar.xz

RUN \
  curl -sL -o /tmp/parallel-20150922.tar.bz2 http://ftpmirror.gnu.org/parallel/parallel-20150922.tar.bz2 && \
  bzip2 -dc parallel-20150922.tar.bz2 | tar xvf - && \
  cd parallel-20150922 && \
  ./configure && make && make install && \
  mkdir -p ~/.parallel && \
  touch ~/.parallel/will-cite && \
  cd /tmp && \
  rm -rf parallel-20150922

RUN \
  curl -sL -o /usr/local/bin/docker-compose https://github.com/docker/compose/releases/download/1.17.1/docker-compose-Linux-x86_64 && \
  chmod +x /usr/local/bin/docker-compose

RUN \
  curl -sL -o /tmp/ruby-2.2.2.tar.gz http://cache.ruby-lang.org/pub/ruby/2.2/ruby-2.2.2.tar.gz && \
  curl -sL -o /tmp/ruby-2.3.3.tar.gz http://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.3.tar.gz && \
  curl -sL -o /tmp/ruby-2.4.0.tar.gz http://cache.ruby-lang.org/pub/ruby/2.4/ruby-2.4.0.tar.gz && \
  tar -xzf ruby-2.2.2.tar.gz && \
  cd ruby-2.2.2 && \
  ./configure --prefix=/opt/rubies/ruby-2.2.2 --with-readline-dir=/usr/lib/x86_64-linux-gnu && \
  make && \
  make install && \
  cd /tmp && \
  rm -rf ruby-2.2.2 && \
  rm -f ruby-2.2.2.tar.gz && \
  tar -xzf ruby-2.3.3.tar.gz && \
  cd ruby-2.3.3 && \
  ./configure --prefix=/opt/rubies/ruby-2.3.3 --with-readline-dir=/usr/lib/x86_64-linux-gnu && \
  make && \
  make install && \
  cd /tmp && \
  rm -rf ruby-2.3.3 && \
  rm -f ruby-2.3.3.tar.gz && \
  tar -xzf ruby-2.4.0.tar.gz && \
  cd ruby-2.4.0 && \
  ./configure --prefix=/opt/rubies/ruby-2.4.0 --with-readline-dir=/usr/lib/x86_64-linux-gnu && \
  make && \
  make install && \
  cd /tmp && \
  rm -rf ruby-2.4.0 && \
  rm -f ruby-2.4.0.tar.gz


RUN \
  . /usr/local/share/chruby/chruby.sh && \
  chruby 2.2.2 && \
  gem install bundler --no-ri --no-rdoc && \
  bundle config --global jobs $(cat /proc/cpuinfo | grep -c processor) && \
  chruby 2.3.3 && \
  gem install -N bundler && \
  bundle config --global jobs $(cat /proc/cpuinfo | grep -c processor) && \
  chruby 2.4.0 && \
  gem install -N bundler && \
  bundle config --global jobs $(cat /proc/cpuinfo | grep -c processor) && \
  echo 'gem: --no-document' >> ~/.gemrc && \
  cp ~/.gemrc /etc/gemrc && \
  chmod uog+r /etc/gemrc && \
  useradd -m -u 8080 jenkins && \
  usermod -a -G docker jenkins && \
  usermod -a -G staff jenkins && \
  chmod +x /usr/local/bin/run.sh && \
  chown -R jenkins:jenkins /usr/local/bin/* && \
  chown -R jenkins:jenkins /opt/jenkins/*

RUN \
  apt-get update && \
  apt-get install -yq liblua5.1-0-dev

EXPOSE 8080

ENTRYPOINT ["/bin/bash", "/usr/local/bin/run.sh"]
