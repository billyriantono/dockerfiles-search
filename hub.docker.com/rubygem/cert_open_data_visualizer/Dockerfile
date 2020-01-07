FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.0.9

RUN gem install cert_open_data_visualizer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["cert_open_data_visualizer"]
CMD ["--help"]
