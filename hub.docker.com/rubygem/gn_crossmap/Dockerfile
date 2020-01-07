FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=2.2.3

RUN gem install gn_crossmap --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["crossmap"]
CMD ["--help"]
