FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.1

RUN gem install jump --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jump-bin"]
CMD ["--help"]
