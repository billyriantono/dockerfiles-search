FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.7

RUN gem install csexton-twitter_archive --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["twitter_archive"]
CMD ["--help"]
