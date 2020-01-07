FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.4

RUN gem install hwaddr --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["hwaddr-generate.rb"]
CMD ["--help"]
