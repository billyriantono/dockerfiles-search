FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.6

RUN gem install gold --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gold"]
CMD ["--help"]
