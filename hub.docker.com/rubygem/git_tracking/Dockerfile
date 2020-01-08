FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.3

RUN gem install git_tracking --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git_tracking"]
CMD ["--help"]
