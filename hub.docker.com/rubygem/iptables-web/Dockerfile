FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.5.pre8

RUN gem install iptables-web --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["iptables-web"]
CMD ["--help"]
