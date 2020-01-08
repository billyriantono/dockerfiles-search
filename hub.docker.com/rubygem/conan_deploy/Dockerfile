FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install conan_deploy --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["conan"]
CMD ["--help"]
