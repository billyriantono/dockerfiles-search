FROM ruby:2.4.1

COPY Gemfile /Gemfile
RUN bundle install

EXPOSE 4100

CMD ["fake_sqs", "-p", "4100", "--database", "/database.yml", "-o", "aws-sqs"]
