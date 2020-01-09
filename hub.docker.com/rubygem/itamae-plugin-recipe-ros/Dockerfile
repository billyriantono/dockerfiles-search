FROM ruby:2.4

MAINTAINER thinkbot@outlook.de

ENV VERSION=0.2.2

RUN gem install itamae-plugin-recipe-ros --version ${VERSION} --no-format-exec

WORKDIR /tmp

ENTRYPOINT ["create_itamae_ros_templates"]
CMD ["--help"]
