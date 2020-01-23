FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.8

RUN gem install html2tex --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["html2tex"]
CMD ["--help"]
