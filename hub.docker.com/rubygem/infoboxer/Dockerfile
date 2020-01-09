FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.7

RUN gem install infoboxer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["infoboxer"]
CMD ["--help"]
