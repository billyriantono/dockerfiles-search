FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.9

RUN gem install itamae-mitsurin --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["itamae"]
CMD ["--help"]
