FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.0

RUN gem install gitwakatime --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gitwakatime"]
CMD ["--help"]
