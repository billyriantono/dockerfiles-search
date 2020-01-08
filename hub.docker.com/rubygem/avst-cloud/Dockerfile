FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.9

RUN gem install avst-cloud --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["avst-cloud"]
CMD ["--help"]
