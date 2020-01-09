FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.8.1

RUN gem install faml --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["faml"]
CMD ["--help"]
