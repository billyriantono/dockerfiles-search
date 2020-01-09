FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.5

RUN gem install homeq --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hq"]
CMD ["--help"]
