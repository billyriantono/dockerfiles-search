FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.7

RUN gem install csv2hash --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["generate_doc"]
CMD ["--help"]
