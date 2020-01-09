FROM ruby:alpine

WORKDIR /sidekiq-cloudwatch
ADD . /sidekiq-cloudwatch
RUN bundle install --without development test
CMD ["./example.rb"]