FROM ruby:2.6.3
RUN apt-get update -qq && apt-get install -y nodejs postgresql-client
RUN mkdir /users-ms
COPY . /usr/src/app
VOLUME /usr/src/app


WORKDIR /usr/src/app

COPY Gemfile Gemfile
# https://github.com/moby/moby/issues/37965#issuecomment-426853382
RUN true
COPY Gemfile.lock /users-ms/Gemfile.lock
RUN gem install rails
RUN bundle install
COPY . /users-ms

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]

