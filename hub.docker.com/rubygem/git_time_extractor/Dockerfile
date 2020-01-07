FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.2

RUN gem install git_time_extractor --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["git_time_extractor"]
CMD ["--help"]
