FROM birchwoodlangham/ubuntu-base:latest

LABEL maintainer="tan.quach@birchwoodlangham.com"

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
		apt-get -y install openjdk-8-jdk openjdk-8-doc openjdk-8-source maven ant && \
		apt-get clean && \
		rm -rf /var/lib/apt/lists/*
