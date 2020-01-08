FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.1

RUN gem install ipa_reader --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ipa_reader"]
CMD ["--help"]
