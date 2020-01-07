FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.5

RUN gem install fml --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["fml2dae.rb"]
CMD ["--help"]
