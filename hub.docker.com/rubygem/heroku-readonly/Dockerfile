FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install heroku-readonly --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["heroku-readonly"]
CMD ["--help"]
