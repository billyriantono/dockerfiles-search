FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4.3

RUN gem install ansible_tools --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ansible-tools"]
CMD ["--help"]
