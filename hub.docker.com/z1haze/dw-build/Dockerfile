FROM ruby:2.2

ARG VERSION=0.6.2

RUN set -x \
  && apt-get update \
  && apt-get -y install git \
  && rm -rf /var/lib/apt/lists/*

RUN gem install github_cli -v ${VERSION} --no-rdoc --no-ri

WORKDIR /project
ENTRYPOINT ["gcli"]
CMD ["--help"]
