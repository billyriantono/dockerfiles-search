FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.4.9

RUN gem install beer_recipe --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["beer_recipe"]
CMD ["--help"]
