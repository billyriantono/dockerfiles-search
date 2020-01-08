FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.0

RUN gem install do_stuff --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["do_stuff"]
CMD ["--help"]
