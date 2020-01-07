FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.0

RUN gem install ibm_sbdtc_rest --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ibmcloud_admin"]
CMD ["--help"]
