FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.9

RUN gem install image_magick --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["bulk_shrink"]
CMD ["--help"]
