FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.0

RUN gem install gutenberg_rdf --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["rdf"]
CMD ["--help"]
