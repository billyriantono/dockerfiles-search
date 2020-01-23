FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.7

RUN gem install higgs --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["higgs_apply_jlog"]
CMD ["--help"]
