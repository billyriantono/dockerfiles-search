FROM ruby:2.6

RUN gem install rack
COPY config.ru .

CMD ["rackup", "-p", "8000", "-o", "0.0.0.0"]
