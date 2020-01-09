FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2013.5

RUN gem install csv2qif --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["csv2qif"]
CMD ["--help"]
