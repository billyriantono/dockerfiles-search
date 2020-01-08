FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.3.0

RUN gem install jara --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jara"]
CMD ["--help"]
