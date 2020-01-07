FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.5.3.9

RUN gem install GameGrid --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["sh.rb"]
CMD ["--help"]
