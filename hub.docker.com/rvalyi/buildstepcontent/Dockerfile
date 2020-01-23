FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.3

RUN gem install html_validation --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["html_validation"]
CMD ["--help"]
