FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.0

RUN gem install git_editor --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git_editor"]
CMD ["--help"]
