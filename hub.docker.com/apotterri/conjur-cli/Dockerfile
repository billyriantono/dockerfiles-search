FROM phusion/baseimage
MAINTAINER Conjur Inc

RUN apt-get update && apt-get install -y curl ruby ruby-dev

RUN curl -so /tmp/cli.deb https://s3.amazonaws.com/conjur-releases/omnibus/conjur_4.28.0-1_amd64.deb \
    && dpkg -i /tmp/cli.deb \
    && rm /tmp/cli.deb

RUN /opt/conjur/embedded/bin/gem install conjur-asset-host-factory
