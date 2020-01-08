FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.6.9

RUN gem install iron_worker_ng --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["iron_worker"]
CMD ["--help"]
