FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=1.0.0

RUN gem install android_img_resizer --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["android_img_resizer"]
CMD ["--help"]
