FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.4

RUN gem install accutronic --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["accu-encrypt"]
CMD ["--help"]
