FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=4.2.9

RUN gem install assplecake-RedCloth --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["redcloth"]
CMD ["--help"]
