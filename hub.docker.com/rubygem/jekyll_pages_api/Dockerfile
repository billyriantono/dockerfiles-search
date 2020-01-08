FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.6

RUN gem install jekyll_pages_api --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["jekyll_pages_api"]
CMD ["--help"]
