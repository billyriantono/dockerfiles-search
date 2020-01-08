FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.3

RUN gem install googleplay_dev_scraper --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["googleplay_dev_scraper"]
CMD ["--help"]
