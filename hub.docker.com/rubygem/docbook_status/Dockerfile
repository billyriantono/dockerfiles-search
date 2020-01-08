FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.1

RUN gem install docbook_status --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docbook_status"]
CMD ["--help"]
