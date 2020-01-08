FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.8.1

RUN gem install fpm --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fpm"]
CMD ["--help"]
