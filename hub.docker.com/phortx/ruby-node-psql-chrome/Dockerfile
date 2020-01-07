FROM ubuntu:16.04

RUN apt-get update
RUN apt-get -y upgrade

# Install dependencies and postgresql
RUN apt-get update -qq && \
    apt-get -y install debconf sudo cmake postgresql postgresql-contrib libpq-dev \
                       build-essential zlib1g-dev libssl-dev \
                       libreadline6-dev libyaml-dev git-core \
                       libcurl4-openssl-dev libmysqlclient-dev libxslt-dev \
                       libsqlite3-dev libmagickwand-dev imagemagick libicu55 \
                       libxml2-dev libxslt1-dev wget \
                       python python-dev python-pip python-virtualenv curl \
                       gconf-service libasound2 libgconf-2-4 libgtk-3-0 libnspr4 \
                       libx11-xcb1 libxss1 libxtst6 fonts-liberation libappindicator1 \
                       libnss3 xdg-utils autoconf

# Cleanup
RUN rm -rf /var/lib/apt/lists/*

RUN sudo -u postgres /etc/init.d/postgresql start \
  && sudo -u postgres psql --command "ALTER USER postgres WITH PASSWORD 'postgres';"


# Install node
RUN \
  cd /tmp && \
  wget http://nodejs.org/dist/node-latest.tar.gz && \
  tar xvzf node-latest.tar.gz && \
  rm -f node-latest.tar.gz && \
  cd node-v* && \
  ./configure && \
  CXX="g++ -Wno-unused-local-typedefs" make && \
  CXX="g++ -Wno-unused-local-typedefs" make install && \
  cd /tmp && \
  rm -rf /tmp/node-v* && \
  npm install -g npm && \
  echo '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc

RUN npm -g install yarn



# Install ruby
ADD https://cache.ruby-lang.org/pub/ruby/2.5/ruby-2.5.0.tar.gz /tmp/

RUN \
  cd /tmp && \
  tar -xzf ruby-2.5.0.tar.gz  && \
  cd ruby-2.5.0 && \
  ./configure && \
  make && \
  make install && \
  cd .. && \
  rm -rf ruby-2.5.0 && \
  rm -f ruby-2.5.0.tar.gz

RUN gem install bundler rake --no-ri --no-rdoc


# Install Google Chrome
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome-stable_current_amd64.deb
