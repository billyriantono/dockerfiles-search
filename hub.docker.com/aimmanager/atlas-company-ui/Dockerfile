FROM ruby:2.6.1
RUN apt-get update -qq
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && apt-get install -y nodejs
RUN mkdir /active_directory
WORKDIR /active_directory
ENV RAILS_ENV production
ENV RAILS_SERVE_STATIC_FILES true
ENV RAILS_LOG_TO_STDOUT true
COPY Gemfile /active_directory/Gemfile
COPY Gemfile.lock /active_directory/Gemfile.lock
RUN bundle install
COPY . /active_directory
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

# Start the main process.
CMD bundle exec puma -C config/puma.rb -e production --port 3092