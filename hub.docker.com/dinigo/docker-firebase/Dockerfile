# use latest Node LTS
FROM node:carbon-alpine
MAINTAINER Daniel Iñigo <danielinigobanos@gmail.com>

# backport up to date tools
RUN apk update && apk add git zip

# install Firebase CLI
RUN yarn global add firebase-tools
