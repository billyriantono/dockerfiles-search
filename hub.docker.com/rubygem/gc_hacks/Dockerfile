FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install gc_hacks --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dump_heap"]
CMD ["--help"]
