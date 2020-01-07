FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.6.2

RUN gem install app_stack --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["stackup"]
CMD ["--help"]
