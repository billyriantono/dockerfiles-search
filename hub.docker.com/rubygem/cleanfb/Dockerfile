FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.1.9

RUN gem install cleanfb --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cleanfb"]
CMD ["--help"]
