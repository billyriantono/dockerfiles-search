FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.8.8

RUN gem install image_voodoo --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["image_voodoo"]
CMD ["--help"]
