FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.0

RUN gem install happy-commit --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["happy-commit-stats"]
CMD ["--help"]
