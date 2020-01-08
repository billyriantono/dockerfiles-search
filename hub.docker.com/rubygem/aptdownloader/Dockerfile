FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.2

RUN gem install AptDownloader --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["apt_downloader"]
CMD ["--help"]
