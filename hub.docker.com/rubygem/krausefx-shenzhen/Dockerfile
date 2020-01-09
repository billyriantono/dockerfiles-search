FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.14.9

RUN gem install krausefx-shenzhen --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["krausefx-ipa"]
CMD ["--help"]
