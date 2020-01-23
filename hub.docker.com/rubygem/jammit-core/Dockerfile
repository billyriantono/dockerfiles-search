FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.1

RUN gem install jammit-core --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jammit"]
CMD ["--help"]
