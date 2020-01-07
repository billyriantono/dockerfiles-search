FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install csv_filter --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["csv_filter"]
CMD ["--help"]
