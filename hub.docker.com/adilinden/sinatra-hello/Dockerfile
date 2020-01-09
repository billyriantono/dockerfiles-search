FROM ruby:alpine

MAINTAINER Adi Linden <adi@adis.ca>

# Cache bundler
COPY Gemfile* /tmp/
WORKDIR /tmp
RUN bundle install

# Install app
WORKDIR /app
COPY app.rb /app/

# Matches port in app.rb
EXPOSE 80

CMD ["ruby", "app.rb"]
