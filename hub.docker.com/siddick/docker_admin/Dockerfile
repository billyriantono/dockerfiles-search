FROM ruby:2.2

RUN mkdir /app && \
    apt-get update && \
    apt-get install -y nodejs && \
    gem install foreman --no-ri --no-rdoc

WORKDIR /app

ENV PORT=5000 RAILS_ENV=production
EXPOSE 5000

COPY Gemfile Gemfile.lock /app/
RUN bundle install --jobs=10 --deployment


COPY . /app/

RUN bundle exec rake assets:precompile

CMD ["foreman", "start"]
