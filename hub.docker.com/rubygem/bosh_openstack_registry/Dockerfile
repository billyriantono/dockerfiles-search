FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install bosh_openstack_registry --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["openstack_registry"]
CMD ["--help"]
