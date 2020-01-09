# This file describes the standard way to build Docker, using docker
#
# Usage:
#
# # Assemble the full dev environment. This is slow the first time.
# docker build -t docker .
#
# # Mount your source in an interactive container for quick testing:
# docker run -v `pwd`:/go/src/github.com/dotcloud/docker --privileged -i -t docker bash
#
# # Run the test suite:
# docker run --privileged docker hack/make.sh test
#
# # Publish a release:
# docker run --privileged \
#  -e AWS_S3_BUCKET=baz \
#  -e AWS_ACCESS_KEY=foo \
#  -e AWS_SECRET_KEY=bar \
#  -e GPG_PASSPHRASE=gloubiboulga \
#  docker hack/release.sh
#
#

docker-version	0.9.0
FROM	ubuntu:13.10
MAINTAINER	Bill Mitchell <vocatan@github.com> (@vocatan)

# Packaged dependencies
RUN	apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -yq \
	wget \
	--no-install-recommends

# Get and compile LXC 0.8 (since it is the most stable)
RUN	echo "Was booted at `date`" >>/tmp/booted.log

ENV	foo	bar

VOLUME	/tmp/shared:/asdf

