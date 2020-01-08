FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.3

RUN gem install cdn_fu --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cdnfu"]
CMD ["--help"]
