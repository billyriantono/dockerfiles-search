FROM ruby:2.4.1

RUN mkdir -p /app
WORKDIR /app

COPY Gemfile /app/
COPY Gemfile.lock /app/
RUN bundle install

COPY . /app

EXPOSE 9292

CMD ["rackup", "-o", "0.0.0.0"]
