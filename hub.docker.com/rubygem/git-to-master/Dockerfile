FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=3.0.1

RUN gem install git-to-master --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git-to-master"]
CMD ["--help"]
