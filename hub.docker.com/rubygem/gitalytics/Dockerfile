FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3.1

RUN gem install gitalytics --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gitalytics"]
CMD ["--help"]
