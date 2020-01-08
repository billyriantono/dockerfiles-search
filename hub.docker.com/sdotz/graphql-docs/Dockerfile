FROM ruby:2.3.3

RUN gem install bundler

COPY . /graphql-docs

WORKDIR /graphql-docs

RUN bundle config --global silence_root_warning 1 && bundle install

VOLUME ["/graphql-docs/output"]

ENTRYPOINT ["bundle", "exec", "gqldocs"]