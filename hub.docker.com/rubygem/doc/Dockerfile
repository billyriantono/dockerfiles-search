FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.0

RUN gem install doc --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docr"]
CMD ["--help"]
