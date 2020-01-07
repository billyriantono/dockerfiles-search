#
# DroneDB container
#
FROM ubuntu:12.04
MAINTAINER Juanjo Mata <juanjo.mata@gmail.com>

# Versions
ENV DRONEDB_VERSION            agroviz
ENV SQL_API_STABLE_VERSION     1.47.1
ENV WINDSHAFT_STABLE_VERSION   5.2.0

# Configuring locales
ENV DEBIAN_FRONTEND noninteractive
RUN dpkg-reconfigure locales && \
      locale-gen en_US.UTF-8 && \
      update-locale LANG=en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# mount-point for persistence beyond container
VOLUME ["/data"]

# this is a development image by default
ENV ENVIRONMENT development

RUN useradd -m -d /home/cartodb -s /bin/bash cartodb && \
  apt-get update &&\
  apt-get install -y -q \
    autoconf binutils-doc bison build-essential flex \
    software-properties-common \
    python-software-properties \
    python-all-dev \
    automake \
    libtool \
    checkinstall \
    unp \
    vim \
    zip \
    unzip \
    gettext \
    git-core \
    git \
    subversion \
    curl

RUN add-apt-repository ppa:cartodb/postgresql-9.5 && apt-get update
RUN apt-get install -y -q \
  libpq5 \
  libpq-dev \
  postgresql-client-9.5 \
  postgresql-client-common

RUN add-apt-repository ppa:cartodb/gis && apt-get update

RUN apt-get update && \
  apt-get install -y -q \
  proj proj-bin proj-data libproj-dev \
  libjson0 libjson0-dev python-simplejson \
  libgeos-c1v5 libgeos-dev \
  gdal-bin libgdal1-dev libgdal-dev \
  gdal2.1-static-bin \
  liblwgeom-2.2.2 postgis postgresql-9.5-postgis-2.2 postgresql-9.5-postgis-scripts

RUN add-apt-repository ppa:ubuntu-toolchain-r/test
RUN add-apt-repository ppa:cartodb/cairo
RUN apt-get update && \
  apt-get install -y -q \
  gcc-4.9 g++-4.8 g++-4.9 \
  make libjpeg-dev libhiredis-dev postgresql-plpython-9.5

RUN apt-get update && \
  apt-get install -y -q \
    ca-certificates \
    redis-server \
    python2.7-dev \
    python-setuptools \
    varnish \
    imagemagick \
    openssl \
    libreadline6 \
    zlib1g \
    zlib1g-dev \
    libssl-dev \
    libyaml-dev \
    libsqlite3-dev \
    sqlite3 \
    libxml2-dev \
    libxslt-dev \
    libc6-dev \
    ncurses-dev \
    pkg-config \
    libpq5 \
    libpq-dev \
    libcurl4-gnutls-dev \
    libffi-dev \
    libgdbm-dev \
    gnupg \
    libreadline6-dev \
    libcairo2-dev \
    libjpeg8-dev \
    libpango1.0-dev \
    libgif-dev \
    libgmp-dev \
    libicu-dev \
  --no-install-recommends &&\
  rm -rf /var/lib/apt/lists/*

# Install NodeJS & update npm
RUN curl https://nodejs.org/download/release/v6.9.2/node-v6.9.2-linux-x64.tar.gz | \
      tar -zxf - --strip-components=1 -C /usr && npm install -g npm@3.10.9 && npm install mkdirp@latest

# Install rvm
ENV PATH $PATH:/usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
#RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3 && \
RUN gpg --keyserver hkp://http-keys.gnupg.net/ --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 && \
    curl -L https://raw.githubusercontent.com/wayneeseguin/rvm/stable/binscripts/rvm-installer | bash -s stable --ruby && \
    echo 'source /usr/local/rvm/scripts/rvm' >> /etc/bash.bashrc && \
    /bin/bash -l -c rvm requirements && \
    echo rvm_max_time_flag=15 >> ~/.rvmrc && \
    /bin/bash -l -c 'rvm install 2.2.3' && \
    /bin/bash -l -c 'rvm use 2.2.3 --default' && \
    /bin/bash -l -c 'gem install bundle archive-tar-minitar'

# Install bundler
RUN /bin/bash -l -c 'gem install bundler --no-doc --no-ri'

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && \
  apt-get install -y -q \
  yarn=0.27.5-1

# Install CartoDB API
ENV CXX=g++-4.8
RUN git clone https://github.com/CartoDB/CartoDB-SQL-API.git && \
      cd CartoDB-SQL-API && git checkout tags/$SQL_API_STABLE_VERSION && ./configure && npm install

# Install Windshaft
ENV NPROCS=1 JOBS=1 CXX=g++-4.9
RUN git clone https://github.com/CartoDB/Windshaft-cartodb.git && \
      cd Windshaft-cartodb && git checkout tags/$WINDSHAFT_STABLE_VERSION && yarn && mkdir logs

# Install CartoDB-NodeJS
RUN git clone https://github.com/CartoDB/cartodb-nodejs.git && \
      cd cartodb-nodejs && npm install cartodb -g

# Install DroneDB
RUN git clone https://github.com/splashblot/dronedb.git dronedb && \
      cd dronedb && mkdir log && git checkout $DRONEDB_VERSION && \
      cp config/grunt_development.json ./config/grunt_true.json && \
      /bin/bash -l -c 'bundle update thin' && \
      /bin/bash -l -c 'bundle install' && \
      cd /dronedb && git submodule update --init --recursive && npm install && \
      cd /dronedb && npm update cartodb.js

ENV CDB_LATEST_VERSION 0.20.0
# ^^^ Informational only, make sure to keep in sync with
# https://github.com/splashblot/docker-postgis/blob/master/Dockerfile.template#L6

# Run Grunt for assets
ENV PATH /dronedb/node_modules/grunt-cli/bin:/usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
RUN /bin/bash -l -c 'cd /dronedb && bundle exec grunt'

# Install Python dependencies
ENV CPLUS_INCLUDE_PATH /usr/include/gdal
ENV C_INCLUDE_PATH /usr/include/gdal
ENV PATH /usr/include/gdal:/dronedb/node_modules/grunt-cli/bin:/usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
RUN easy_install --index-url=https://pypi.python.org/simple/ pip && cd /dronedb && pip install --no-binary :all: -r python_requirements.txt

# Install god for monitoring resque
RUN /bin/bash -l -c 'gem install god'

# Copy configs
ADD ./config/CartoDB-dev.js          /CartoDB-SQL-API/config/environments/development.js
ADD ./config/CartoDB-staging.js      /CartoDB-SQL-API/config/environments/staging.js
ADD ./config/CartoDB-prod.js          /CartoDB-SQL-API/config/environments/production.js
ADD ./config/WS-dev.js.envsubst      /Windshaft-cartodb/config/environments/development.js.envsubst
ADD ./config/WS-staging.js.envsubst  /Windshaft-cartodb/config/environments/staging.js.envsubst
ADD ./config/WS-prod.js.envsubst     /Windshaft-cartodb/config/environments/production.js.envsubst
ADD ./config/app_config.yml.envsubst /dronedb/config/app_config.yml.envsubst
ADD ./config/database.yml            /dronedb/config/database.yml
ADD ./create_db_only.sh              /dronedb/script/create_db_only.sh
ADD ./setup_tiles_feature_flags.sh   /dronedb/script/setup_tiles_feature_flags.sh
ADD ./create_tiles_dev_user.sh       /dronedb/script/create_tiles_dev_user.sh
ADD ./setup_organization.sh          /dronedb/script/setup_organization.sh
ADD ./setup_geocoder.sh              /dronedb/script/setup_geocoder.sh
ADD ./fill_geocoder.sh               /dronedb/script/fill_geocoder.sh

# Sample crontab.txt (see ./startup.sh)
# ADD ./tiles/crontab.txt              /dronedb/script/tiles/crontab.txt

# Put Tiles sample data in place
ADD ./tiles/sampledata               /dronedb/script/tiles_sampledata

# New Relic Postgres plugin
RUN /bin/bash -l -c 'gem install newrelic_postgres_plugin'
RUN mkdir -p /opt/newrelic/postgres
ADD ./config/postgres_newrelic_plugin.yml.envsubst \
      /opt/newrelic/postgres/config/newrelic_plugin.yml.envsubst

# Expose CartoDB ports
EXPOSE 3000 8080 8181

ENV GDAL_DATA /usr/share/gdal/2.1

RUN mkdir -p /cartodb/log && touch /cartodb/log/users_modifications
ADD ./startup.sh /opt/startup.sh

CMD ["/bin/bash", "/opt/startup.sh"]
