FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.4

RUN gem install autoversion --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["autoversion"]
CMD ["--help"]
