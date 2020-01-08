FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.2

RUN gem install cfndsl --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cfndsl"]
CMD ["--help"]
