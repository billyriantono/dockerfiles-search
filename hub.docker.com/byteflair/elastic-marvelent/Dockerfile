# Official Docker python image
FROM python:2.7.8
MAINTAINER Bryan Shelton <bryan@sheltonplace.com>

# Add the nodejs repo
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash -

RUN apt-get update && apt-get install -y \
    fontconfig \
    geoip-database \
    gettext \
    less \
    libcurl4-gnutls-dev \
    libgeoip1 \
    libgeos-dev \
    libspatialite-dev \
    libtidy-dev \
    libxft-dev \
    mysql-client \
    nodejs \
    postgresql-client \
    ruby \
    ruby-dev \
    sqlite3 \
    swig \
    vim \
    && rm -rf /var/lib/apt/lists/*

# Upgrade virtualenv and setuptools
RUN pip install virtualenv --upgrade
RUN pip install setuptools --upgrade

# Scss/sass dependencies
RUN gem install sass -v 3.4.5 --no-rdoc --no-ri
RUN gem install compass -v 1.0.1 --no-rdoc --no-ri
