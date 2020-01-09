FROM ruby:2.3.1-slim

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN gem update --system && gem install bundler 

RUN apt-get update -qq && apt-get install -y build-essential 

# for postgres
RUN apt-get install -y libpq-dev

# for nokogiri
RUN apt-get install -y libxml2-dev libxslt1-dev

# for capybara-webkit
RUN apt-get install -y libqt4-webkit libqt4-dev xvfb

# for a JS runtime
RUN apt-get install -y nodejs

EXPOSE 3000
ENV RAILS_LOG_TO_STDOUT=1 RAILS_SERVE_STATIC_FILES=1

COPY Gemfile /usr/src/app/
COPY Gemfile.lock /usr/src/app/
RUN bundle install

COPY . /usr/src/app
RUN RAILS_ENV=production SECRET_KEY_BASE=none MAIL_URL_HOST=none \
	bin/rake assets:precompile

CMD ["bin/rails", "server", "-b", "0.0.0.0", "-p", "3000"]
