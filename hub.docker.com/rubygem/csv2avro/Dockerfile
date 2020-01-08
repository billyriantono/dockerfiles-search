FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3.1

RUN gem install csv2avro --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["csv2avro"]
CMD ["--help"]
