FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.8

RUN gem install codefumes_harvester --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cf_harvest_repo_metrics"]
CMD ["--help"]
