FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.5

RUN gem install a14z6ch_elapsed_days --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["a14z6ch_elapsed_days"]
CMD ["--help"]
