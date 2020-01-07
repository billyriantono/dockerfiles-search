FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.6.2

RUN gem install easypost --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["easypost-irb"]
CMD ["--help"]
