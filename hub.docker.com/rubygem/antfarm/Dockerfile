FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.5.0.beta2

RUN gem install antfarm --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["antfarm"]
CMD ["--help"]
