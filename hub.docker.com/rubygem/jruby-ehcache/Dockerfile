FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3.2

RUN gem install jruby-ehcache --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ehcache"]
CMD ["--help"]
