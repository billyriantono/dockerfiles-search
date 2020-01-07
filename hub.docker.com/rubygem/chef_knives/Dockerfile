FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.1

RUN gem install chef_knives --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["chef_node_find"]
CMD ["--help"]
