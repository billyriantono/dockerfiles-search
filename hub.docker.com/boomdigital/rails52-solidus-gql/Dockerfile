FROM ruby:2.5.1


ARG RDS_DB_NAME=SOLIDUS_DEMO
ARG RDS_USERNAME=postgres
ARG RDS_PASSWORD=postgres
ARG RDS_HOSTNAME=postgres
ARG RDS_PORT=5432
ARG RDS_MAX_THREADS=6



RUN apt-get update && apt-get install -y nodejs postgresql-client sqlite3 vim --no-install-recommends && rm -rf /var/lib/apt/lists/*


RUN mkdir /app
COPY . /app
COPY Gemfile /app/
COPY Gemfile.lock /app/
COPY Rakefile /app/Rakefile

WORKDIR /app
RUN bundle install

RUN bundle exec rake assets:precompile





EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
