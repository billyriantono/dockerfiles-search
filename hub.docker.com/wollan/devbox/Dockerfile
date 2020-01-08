#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "update.sh"
# PLEASE DO NOT EDIT IT DIRECTLY.
# MAKE CHANGES TO Dockerfile.template INSTEAD.
#
FROM ubuntu:18.04
MAINTAINER Andreas Wohlén <andreas.wohlen@gmail.com>

RUN apt-get update \
 && apt-get install -y --no-install-recommends \
	docker.io \
	curl \
	git \
	iputils-ping \
	vim \
	less \
	jq \
	python \
	python3 \
	sudo \
	ca-certificates \
	host \
	net-tools \
    openssh-client \
    nmap \
    file \
 && rm -rf /var/lib/apt/lists/*

#set docker cli api version to match daemon if mismatch
RUN echo "export DOCKER_API_VERSION=\$(docker version 2> >(grep -Po '\d+\.\d+' | tail -n 1) >/dev/null)" >> /root/.bashrc \
 && printf '$include /etc/inputrc\nset completion-ignore-case On\n' > /root/.inputrc

