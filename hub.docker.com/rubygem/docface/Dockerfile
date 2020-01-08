FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.7

RUN gem install docface --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docface"]
CMD ["--help"]
