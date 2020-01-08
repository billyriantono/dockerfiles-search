FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=7.0.1

RUN gem install gman --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gman"]
CMD ["--help"]
