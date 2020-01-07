FROM iron/ruby

MAINTAINER Vicky Gray <vickygray26@hotmail.com>

RUN apk --update add ruby-rdoc ruby-irb

RUN gem install bundler

ADD /unicorn /unicorn

EXPOSE 8080

WORKDIR /unicorn

RUN bundle install

CMD bundle exec rackup --port 8080 --host 0.0.0.0

RUN curl http://unicornpoo.herokuapp.com/update/team2-teethbrains/complete
