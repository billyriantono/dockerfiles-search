FROM ruby:2.5.3-alpine

RUN apk update

COPY ./random_generate.rb ./usr/local/bin/random_generate.rb

RUN chmod 0755 /usr/local/bin/random_generate.rb

ENTRYPOINT ["ruby", "./usr/local/bin/random_generate.rb"]