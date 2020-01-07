FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install getversion --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["getversion.rb"]
CMD ["--help"]
