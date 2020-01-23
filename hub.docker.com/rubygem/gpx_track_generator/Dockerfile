FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.3.5

RUN gem install gpx_track_generator --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["gpx_track"]
CMD ["--help"]
