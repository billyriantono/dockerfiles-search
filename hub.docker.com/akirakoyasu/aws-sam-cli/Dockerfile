# Run SAM CLI in a container
#
# docker run --rm \
#   -e SAM_DOCKER_VOLUME_BASEDIR=${PWD}/path/to/module/root \
#   -v ${PWD}:/var/lib/sam-cli \
#   -v /var/run/docker.sock:/var/run/docker.sock \
#   --name sam-cli \
#   akirakoyasu/aws-sam-cli \
#   --version
#

FROM python:3.6-slim
LABEL maintainer="Akira Koyasu <mail@akirakoyasu.net>"

ARG sam_cli_version="0.16.1"

WORKDIR /var/lib/sam-cli

RUN set -ex \
  && savedAptMark="$(apt-mark showmanual)" \
  && apt-get update -qq && apt-get install -y --no-install-recommends \
  		gcc \
  		libc6-dev \
  \
  && pip install aws-sam-cli==${sam_cli_version} \
  \
	&& apt-mark auto '.*' > /dev/null \
	&& apt-mark manual $savedAptMark \
	&& apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
  	&& rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["sam"]
