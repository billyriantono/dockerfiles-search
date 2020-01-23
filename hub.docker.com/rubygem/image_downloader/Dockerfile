FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.4

RUN gem install image_downloader --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["download_any_images"]
CMD ["--help"]
