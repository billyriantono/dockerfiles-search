FROM jenkins/jenkins:lts
LABEL maintainer="Wonderlic DevOps <DevOps@wonderlic.com>"

USER root

RUN \
	apt-get update && \
	apt-get install -y --no-install-recommends zstd g++ build-essential libsecret-1-0 && \
	rm -rf /var/lib/apt/lists/*

USER jenkins
