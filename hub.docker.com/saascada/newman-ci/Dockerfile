# Image Located: Dockerhub - saascada/newman-ci
# Build: docker build -t saascada/newman-ci .
# Push: docker push saascada/nemwman-ci
FROM node:10.15.3-alpine
LABEL maintainer="developers@saescada.com"
RUN apk update
RUN apk -Uuv --no-cache add npm
RUN rm /var/cache/apk/*
RUN npm i newman -g