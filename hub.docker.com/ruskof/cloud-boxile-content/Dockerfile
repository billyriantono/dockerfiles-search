FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.9

RUN gem install haml-i18n-extractor --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["haml-i18n-extractor"]
CMD ["--help"]
