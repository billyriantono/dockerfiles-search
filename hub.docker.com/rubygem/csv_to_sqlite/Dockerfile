FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install csv_to_sqlite --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["csv_to_sqlite"]
CMD ["--help"]
