FROM ruby:2.5

RUN bundle config --global frozen 1

ENV PORT=4567

WORKDIR /usr/src/app
COPY Gemfile Gemfile.lock ./
RUN bundle install

COPY . .

CMD /usr/local/bin/ruby ./app.rb -o 0.0.0.0 -p $PORT
EXPOSE $PORT