FROM ubuntu:zesty
MAINTAINER Chris Weyl <cweyl@alumni.drew.edu>

ENV DEBIAN_FRONTEND=noninteractive

RUN \
	apt-get update && \
		apt-get -y install shellcheck && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/*

ENTRYPOINT [ "shellcheck", "-" ]
