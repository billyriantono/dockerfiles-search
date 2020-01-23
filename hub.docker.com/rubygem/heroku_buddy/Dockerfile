FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.8

RUN gem install heroku_buddy --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["h"]
CMD ["--help"]
