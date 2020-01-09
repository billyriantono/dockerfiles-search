FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install diana --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["diana"]
CMD ["--help"]
