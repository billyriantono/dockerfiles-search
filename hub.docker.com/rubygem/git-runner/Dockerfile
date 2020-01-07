FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.3.2

RUN gem install git-runner --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-runner"]
CMD ["--help"]
