#
# Next.js 4.2 Build Image
# Docker image with libraries and tools as required for building Next.js 4.2 projects using Yarn 
#

FROM node:9.4.0-alpine
MAINTAINER Agile Digital <info@agiledigital.com.au>
LABEL Description="Docker image with libraries and tools as required for building Next.js 4.2 projects using Yarn" Vendor="Agile Digital" Version="0.1"

ENV HOME /home/jenkins

RUN apk add --update --no-cache openjdk8-jre

RUN addgroup -S -g 10000 jenkins
RUN adduser -S -u 10000 -h $HOME -G jenkins jenkins

WORKDIR /home/jenkins
USER jenkins