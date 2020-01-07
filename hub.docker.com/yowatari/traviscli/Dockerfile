FROM ruby:2.0.0

ARG CLI_VERSION=1.8.9
ARG LINT_VERSION=2.0.0

RUN set -x \
    && apt-get update \
    && apt-get -y install git \
    && rm -rf /var/lib/apt/lists/*

RUN set -x \
    && gem install travis -v ${CLI_VERSION} --no-rdoc --no-ri \
    && gem install travis-cli-gh --no-rdoc --no-ri \
    && gem install travis-lint -v ${LINT_VERSION} --no-rdoc --no-ri

WORKDIR /project
ENTRYPOINT ["travis"]
CMD ["help", "--no-interactive"]
