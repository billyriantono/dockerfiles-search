FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.1

RUN gem install hlspider --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hlspider"]
CMD ["--help"]
