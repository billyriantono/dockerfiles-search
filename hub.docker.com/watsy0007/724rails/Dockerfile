FROM ruby:2.4.2

RUN mkdir /app
WORKDIR /app

ADD Gemfile /app
RUN bundle install

CMD ["bash"]
