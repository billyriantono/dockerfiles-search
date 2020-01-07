FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install doc_to_dash --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["doc_to_dash"]
CMD ["--help"]
