FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.6.9

RUN gem install circonus --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["circonus-add-http-check"]
CMD ["--help"]
