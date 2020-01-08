FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.0

RUN gem install code_poetry --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["code_poetry"]
CMD ["--help"]
