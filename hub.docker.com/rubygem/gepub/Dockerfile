FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.7.0beta3

RUN gem install gepub --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["genepub"]
CMD ["--help"]
