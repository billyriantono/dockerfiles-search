FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.2

RUN gem install gmail_sender --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gmail"]
CMD ["--help"]
