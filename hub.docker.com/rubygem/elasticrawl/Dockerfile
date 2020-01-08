FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.8

RUN gem install elasticrawl --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["elasticrawl"]
CMD ["--help"]
