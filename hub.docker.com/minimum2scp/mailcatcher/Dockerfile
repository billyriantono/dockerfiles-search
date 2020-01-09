FROM ruby:2.6.5
WORKDIR /usr/app/mailcatcher/
ADD Gemfile Gemfile.lock /usr/app/mailcatcher/
RUN bundle install --system
EXPOSE 1025 1080
CMD bundle exec mailcatcher -f --ip 0.0.0.0
