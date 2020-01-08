FROM fluent/fluentd:v1.7-debian
MAINTAINER devops@broadinstitute.org

USER root

# copy Gemfile with plugins into container
COPY Gemfile /Gemfile

# put Dockerfile in container so its easy to tell how it was built
COPY Dockerfile /Dockerfile

# Need to re-install build tools in order to install additional fluentd Gem plugins
RUN  apt-get update \
 && buildDeps=" \
      make gcc g++ libc-dev \
      wget bzip2 gnupg dirmngr \
    " \
 && apt-get install -y --no-install-recommends $buildDeps \
 && gem install --file /Gemfile \
 && gem sources --clear-all \
 && apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
                  $buildDeps \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /home/fluent/.gem/ruby/2.5.0/cache/*.gem

COPY fluent.conf /fluentd/etc/fluent.conf

# USER fluent
