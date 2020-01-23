FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install img_dl --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["img_dl"]
CMD ["--help"]
