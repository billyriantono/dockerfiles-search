FROM woahbase/alpine-webhook:x86_64

ARG DOCKER_CLI_VERSION="18.03.1-ce"

RUN cd $(mktemp -d) &&\
  curl -L https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_CLI_VERSION}.tgz | tar xz &&\
  mv docker/docker /usr/local/bin/ &&\
  rm -rf docker
