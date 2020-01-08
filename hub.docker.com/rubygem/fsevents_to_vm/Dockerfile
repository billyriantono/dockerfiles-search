FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.3

RUN gem install fsevents_to_vm --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fsevents_to_vm"]
CMD ["--help"]
