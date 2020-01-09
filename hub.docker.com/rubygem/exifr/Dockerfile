FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.5

RUN gem install exifr --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["exifr"]
CMD ["--help"]
