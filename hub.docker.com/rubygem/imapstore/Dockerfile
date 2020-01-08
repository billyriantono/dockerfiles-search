FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.2

RUN gem install imapstore --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["imapstore"]
CMD ["--help"]
