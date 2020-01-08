FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.8.0.alpha1

RUN gem install docsplit --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["docsplit"]
CMD ["--help"]
