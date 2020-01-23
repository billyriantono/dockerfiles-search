FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.6

RUN gem install google_refine --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["upload-to-refine"]
CMD ["--help"]
