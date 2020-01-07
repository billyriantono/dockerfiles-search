FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.6

RUN gem install itrp-export-monitor --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["itrp-export-monitor"]
CMD ["--help"]
