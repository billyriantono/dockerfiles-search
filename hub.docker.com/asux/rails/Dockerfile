FROM ruby:2.3
MAINTAINER Alex Ulianytskyi <a.ulyanitsky@gmail.com>

# Packages
ENV MAIN_PACKAGES git postgresql-client mysql-client
# ENV BUILD_DEPENDENCIES
# Gems to install
ENV DEFAULT_GEMS rails slack-notifier puma pg mysql2 bcrypt

# Install main packages
RUN apt-get update
RUN apt-get install -yq ${MAIN_PACKAGES} ${BUILD_DEPENDENCIES}

# Pre-install gems
RUN gem install ${DEFAULT_GEMS}

# Removing build dependencies, clean temporary files
# RUN apt-get purge -yq ${BUILD_DEPENDENCIES}

# Make sure main packages installed
RUN apt-get install -yq ${MAIN_PACKAGES}

RUN apt-get autoremove -yq \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN rails --version
RUN puma --version
RUN psql --version
RUN mysql --version

# throw errors if Gemfile has been modified since Gemfile.lock
# RUN bundle config --global frozen 1

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

EXPOSE 3000
CMD bin/start.sh
