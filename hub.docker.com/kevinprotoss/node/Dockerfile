FROM node:8.7.0-alpine

LABEL maintainer "Junxiang Wei <kevinprotoss.wei@gmail.com>"

# Add utils for compiling dependencies
RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh make gcc g++ python