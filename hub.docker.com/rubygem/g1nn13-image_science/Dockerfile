FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.2.9

RUN gem install g1nn13-image_science --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["image_science_thumb"]
CMD ["--help"]
