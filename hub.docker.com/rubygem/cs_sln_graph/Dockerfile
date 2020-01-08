FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.6

RUN gem install cs_sln_graph --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cs_sln_graph"]
CMD ["--help"]
