FROM ruby:2.5.1
MAINTAINER Kevin Traver (Greenstone Homes)

RUN apt-get update && apt-get install -y nodejs --no-install-recommends
RUN apt-get update && apt-get install -y sqlite --no-install-recommends

RUN gem install bundler --no-ri --no-rdoc

RUN apt-get update && apt-get install -y build-essential --no-install-recommends
RUN apt-get update && apt-get install -y libc6-dev --no-install-recommends

WORKDIR /tmp
RUN wget ftp://ftp.freetds.org/pub/freetds/stable/freetds-1.00.80.tar.gz
RUN tar -xzf freetds-1.00.80.tar.gz
WORKDIR /tmp/freetds-1.00.80
RUN ./configure --prefix=/usr/local --with-tdsver=7.3
RUN make
RUN make install

WORKDIR /

ADD Gemfile Gemfile

RUN bundle install

RUN rm Gemfile
RUN rm Gemfile.lock

CMD ["bundle install"]

RUN rm -rf /tmp/*
