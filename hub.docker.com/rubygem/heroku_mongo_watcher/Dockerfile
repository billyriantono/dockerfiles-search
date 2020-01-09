FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.0

RUN gem install heroku_mongo_watcher --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["watcher"]
CMD ["--help"]
