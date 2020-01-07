FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.1.0.5

RUN gem install dotless --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["dotless"]
CMD ["--help"]
