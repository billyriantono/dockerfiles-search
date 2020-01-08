FROM node:current-stretch-slim
LABEL maintainer="docker@public.swineson.me"
RUN apt-get update \
	&& apt-get install -y sudo \
	&& rm -rf /var/lib/apt/lists/*
