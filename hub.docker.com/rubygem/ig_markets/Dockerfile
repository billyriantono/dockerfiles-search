FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9

RUN gem install ig_markets --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ig_markets"]
CMD ["--help"]
