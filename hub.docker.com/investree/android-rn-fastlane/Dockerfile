FROM investree/android-rn:latest

MAINTAINER Feri Setiyawan <feri.setiyawan@investree.id>

RUN apt-get update && apt-get install --no-install-recommends -y build-essential ruby-dev libcurl4-gnutls-dev git ssh-client

RUN gem install fastlane -NV \
    && gem install bundler

RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN git config --global user.email "automation@fastlane.tools"
RUN git config --global user.name "Fastlane Tools"

RUN apt-get autoremove -y && apt-get clean

