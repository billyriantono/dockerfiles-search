FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.4

RUN gem install html2email --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["html2email"]
CMD ["--help"]
