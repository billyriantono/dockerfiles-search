FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.5

RUN gem install hash-that-tree --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hashthattree"]
CMD ["--help"]
