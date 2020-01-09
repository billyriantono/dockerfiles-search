FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6.2

RUN gem install kitchen-ansiblepush --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["kitchen-ansible-inventory"]
CMD ["--help"]
