FROM ubuntu:xenial
LABEL maintainer="Drew Leske <drew.leske@computecanada.ca>"

ENV DEBIAN_FRONTEND="noninteractive"
ENV NOKOGIRI_USE_SYSTEM_LIBRARIES="true"

# install dev environment and Puppet tools
RUN apt-get -qq update && apt-get -qq -o=Dpkg::Use-Pty=0 install wget gcc libxml2-dev libxslt-dev make ruby ruby-dev git python
RUN wget https://apt.puppetlabs.com/puppetlabs-release-pc1-precise.deb && dpkg -i puppetlabs-release-pc1-precise.deb
RUN apt-get -qq update && apt-get -qq -o=Dpkg::Use-Pty=0 install puppet-agent
RUN gem install --no-rdoc --no-ri pkg-config -v "~> 1.1"
RUN gem install --no-rdoc --no-ri rails-erb-lint puppet-lint
RUN gem install --no-rdoc --no-ri yamllint

# clean up unneeded packages (this doesn't seem to reduce image size)
RUN apt-get -qq remove gcc make wget libicu-dev && apt-get -qq autoremove
