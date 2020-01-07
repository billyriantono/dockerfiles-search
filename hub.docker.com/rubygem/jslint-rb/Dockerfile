FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6

RUN gem install jslint-rb --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jslint-rb"]
CMD ["--help"]
