FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.4.0

RUN gem install Ifd_Mobile --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["Ifd_Mobile"]
CMD ["--help"]
