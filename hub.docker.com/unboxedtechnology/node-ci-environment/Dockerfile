FROM node:10.15.3
LABEL maintainer="Unboxed Technology LLC, https://unboxedtechnology.com"
LABEL author="Hayden Braxton, haydenbraxton@unboxedtechnology.com"
LABEL repository="unboxedtechnology/node-ci-environment"

ENV NODE_ENV=development
RUN mkdir /opt/app && \
		apt-get update && \
		apt-get install \
		ncftp=2:3.2.5-2