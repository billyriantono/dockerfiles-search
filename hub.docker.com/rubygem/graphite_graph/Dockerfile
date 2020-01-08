FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.8

RUN gem install graphite_graph --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["check_graph.rb"]
CMD ["--help"]
