FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.9

RUN gem install ansible_spec --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ansiblespec-init"]
CMD ["--help"]
