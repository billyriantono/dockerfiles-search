FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.0

RUN gem install ical_punch --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ical_punch"]
CMD ["--help"]
