FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.1.1

RUN gem install ci_uy --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["ci_uy"]
CMD ["--help"]
