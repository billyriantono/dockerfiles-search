FROM litaio/ruby:2.1.2
MAINTAINER Carlos Diaz-Padron
MAINTAINER carlos@carlosdp.io

RUN apt-get -y install libpq-dev nodejs

RUN gem install bundler --no-ri --no-rdoc

WORKDIR /tmp 
ADD Gemfile Gemfile
ADD Gemfile.lock Gemfile.lock
RUN bundle install 

ADD . /opt/example

WORKDIR /opt/example
ENV RAILS_ENV production
RUN rake assets:precompile

EXPOSE 80

CMD rails server -p 80
