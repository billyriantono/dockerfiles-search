FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.5

RUN gem install douban.fm --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["douban.fm"]
CMD ["--help"]
