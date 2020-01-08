FROM ubuntu:14.04
MAINTAINER David Siaw "david.siaw@mobingi.com"

RUN apt-get -yqq update \
  && apt-get -yqq install curl build-essential libxml2-dev libxslt-dev git autoconf

RUN curl -L https://www.opscode.com/chef/install.sh \
  | bash > /dev/null
  
RUN /opt/chef/embedded/bin/gem install berkshelf > /dev/null
