# We use this base-image to increase build speed
# This Dockerfile is linked to the docker hub (automated builds) on `master` branch
# on `https://hub.docker.com/r/simplifield/alpine-lerna`
# In case, if you want to try something on your own branch, you can always do
# 1) `docker images`, find this image and remove it with `docker rmi -f <image_id>`
# 2) do `docker build <path to this Dockerfile> --tag <name of just removed image>`
# 3) rebuild your containers
# So now your containers will use your LOCAL version of this base image instead of docker hub's version

FROM node:8-alpine

RUN set -x

# "native-deps" is a virtual name which can be used to simply remove all following packages (starting from "git")
RUN apk --no-cache --update add --virtual \
  native-deps \
  git \
  curl \
  bash \
  openssh \
  g++ \
  gcc \
  libgcc \
  libstdc++ \
  linux-headers \
  make \
  python

RUN curl -sL https://github.com/DarthHater/docker-phantomjs2/releases/download/2.1.1/dockerized-phantomjs.tar.gz | tar xz -C /
RUN phantomjs --version
RUN curl -sL https://sentry.io/get-cli/ | bash
RUN npm install --quiet node-gyp -g
RUN npm install -g lerna

# clean up stuff
RUN rm -rf /var/cache/apk/*

# @TODO try AND TEST multistage here. Is it also actual for base images?
