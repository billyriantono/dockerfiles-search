FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.5

RUN gem install digiusb --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["digiterm"]
CMD ["--help"]
