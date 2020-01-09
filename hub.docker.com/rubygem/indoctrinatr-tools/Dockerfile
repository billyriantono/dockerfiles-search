FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9.0

RUN gem install indoctrinatr-tools --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["indoctrinatr"]
CMD ["--help"]
