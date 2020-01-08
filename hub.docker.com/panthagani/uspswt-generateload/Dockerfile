FROM ruby:2.5.3

ENV APP_HOME /myapp
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

ADD ziplookup/Gemfile* $APP_HOME/

RUN gem install bundler

RUN apt-get update
RUN apt-get install nodejs -y

ADD ziplookup $APP_HOME
RUN gem install nokogiri -v '1.10.3'
RUN gem install nio4r -v '2.4.0'
RUN gem install websocket-driver -v '0.7.1'
RUN gem install bindex -v '0.8.1'
RUN gem install msgpack -v '1.3.0'
RUN gem install bootsnap -v '1.4.4'
RUN gem install byebug -v '11.0.1'
RUN gem install childprocess -v '1.0.1'
RUN gem install ffi -v '1.11.1'
RUN gem install puma -v '4.0.1'
RUN bundle install

EXPOSE 5004
CMD ["rails", "server", "-b", "0.0.0.0"]
