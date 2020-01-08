FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.5.0-x86-mingw32

RUN gem install amalgalite --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["amalgalite-pack"]
CMD ["--help"]
