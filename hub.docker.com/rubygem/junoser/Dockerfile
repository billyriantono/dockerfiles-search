FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.4

RUN gem install junoser --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["junoser"]
CMD ["--help"]
