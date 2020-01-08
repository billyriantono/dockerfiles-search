FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.3

RUN gem install ansible_eyc_inventory --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ansible_eyc_inventory"]
CMD ["--help"]
