FROM ruby:latest

# throw errors if Gemfile has been modified since Gemfile.lock
# RUN bundle config --global frozen 1

WORKDIR /usr/src/app/

COPY Gemfile ./
# COPY Gemfile.lock ./
RUN bundle install

ADD . /usr/src/app/

EXPOSE 4567

CMD ["rerun", "ruby /usr/src/app/app.rb"]