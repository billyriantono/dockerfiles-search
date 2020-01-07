FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=4.3.3

RUN gem install jspec --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jspec"]
CMD ["--help"]
