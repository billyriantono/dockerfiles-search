FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.1

RUN gem install kablame --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-kablame"]
CMD ["--help"]
