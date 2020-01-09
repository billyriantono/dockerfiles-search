FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.9

RUN gem install factor --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["factor"]
CMD ["--help"]
