FROM redbadger/base:latest

RUN \
  DEBIAN_FRONTEND=noninteractive apt-get -y install build-essential curl libcurl4-openssl-dev libreadline-dev libssl-dev libxml2-dev libxslt1-dev libyaml-dev zlib1g-dev libpq-dev &&\
  curl -O http://ftp.ruby-lang.org/pub/ruby/2.1/ruby-2.1.2.tar.gz &&\
  tar -zxvf ruby-2.1.2.tar.gz &&\
  cd ruby-2.1.2 &&\
  ./configure --disable-install-doc &&\
  make &&\
  make install &&\
  cd .. &&\
  rm -r ruby-2.1.2 ruby-2.1.2.tar.gz &&\
  echo 'gem: --no-rdoc --no-ri' > /usr/local/etc/gemrc &&\
  gem install bundler