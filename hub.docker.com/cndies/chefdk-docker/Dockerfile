ARG CHEFDK=latest
FROM chef/chefdk:$CHEFDK
LABEL version="0.1" maintainer="cndies"

ARG DOCKERVERSION=18.09.1

# Install docker client
RUN curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKERVERSION}.tgz \
  && mv docker-${DOCKERVERSION}.tgz docker.tgz \
  && tar xzvf docker.tgz \
  && mv docker/docker /usr/local/bin \
  && rm -r docker docker.tgz

# Install Docker driver Test kitchen
RUN chef gem install kitchen-docker

WORKDIR /
