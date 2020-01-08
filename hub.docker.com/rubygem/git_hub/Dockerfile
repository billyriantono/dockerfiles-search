FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.0

RUN gem install git_hub --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git_hub"]
CMD ["--help"]
