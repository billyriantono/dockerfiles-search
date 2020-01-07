FROM roovo/ubuntu:12.04

MAINTAINER roovo "roovo@roovoweb.com"

RUN \
  echo "export RUBY_BUILD_VERSION=20140110.1" >> /.profile ;\
  . /.profile ;\
  apt-get install build-essential libffi-dev libreadline-dev libyaml-dev zlib1g-dev ;\
  apt-get install libssl-dev libcurl4-openssl-dev curl openssl ca-certificates ;\
  apt-get install libxml2 libxml2-dev libxslt1-dev ;\
  apt-get clean ;\
  ruby_build_url="https://github.com/sstephenson/ruby-build/archive/v$RUBY_BUILD_VERSION.tar.gz" ;\
  wget -O - $ruby_build_url | tar -C /usr/local/src -zxv ;\
  cd /usr/local/src/ruby-build-$RUBY_BUILD_VERSION && sh install.sh ;\
  rm -rf /usr/local/src
# END RUN
