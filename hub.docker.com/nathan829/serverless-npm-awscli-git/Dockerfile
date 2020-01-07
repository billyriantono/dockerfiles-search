FROM node:8-alpine

RUN apk update
RUN apk add git curl bash make openssh zip coreutils grep

# Install serverless
RUN npm install -g serverless@1.51.0

# https://github.com/senseyeio/docker-alpine-aws-cli/blob/master/Dockerfile
RUN apk -Uuv add groff less python py-pip
RUN pip install awscli
RUN apk --purge -v del py-pip
RUN rm /var/cache/apk/*