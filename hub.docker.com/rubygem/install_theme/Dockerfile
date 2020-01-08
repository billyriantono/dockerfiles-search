FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.8.2

RUN gem install install_theme --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["install_theme"]
CMD ["--help"]
