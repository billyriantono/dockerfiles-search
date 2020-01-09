FROM ruby:2.0

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY . /usr/src/app
RUN bundle install

VOLUME /var/data/fakes3
EXPOSE 80

CMD ["bundle", "exec", "bin/fakes3", "-r", "/var/data/fakes3", "-p", "80"] 
