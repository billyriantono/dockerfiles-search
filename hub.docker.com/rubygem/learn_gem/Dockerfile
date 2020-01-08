FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install learn_gem --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["learn_gem"]
CMD ["--help"]
