# We use this base-image to increase build speed
# This Dockerfile is linked to the docker hub (automated builds) on `master` branch
# on `https://hub.docker.com/r/simplifield/node-lerna`
# In case, if you want to try something on your own branch, you can always do
# 1) `docker images`, find this image and remove it with `docker rmi -f <image_id>`
# 2) do `docker build <path to this Dockerfile> --tag <name of just removed image>`
# 3) rebuild your containers
# So now your containers will use your LOCAL version of this base image instead of docker hub's version

FROM node:8.9

RUN set -x

RUN npm install -g lerna

# @TODO try AND TEST multistage here. Is it also actual for base images?
