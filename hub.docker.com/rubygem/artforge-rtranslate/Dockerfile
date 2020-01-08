FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.3.4

RUN gem install artforge-rtranslate --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["rtranslate"]
CMD ["--help"]
