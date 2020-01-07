FROM alpine:latest

LABEL maintainer="Hexosse <hexosse@gmail.com>" \
      description="Minimal Alpine image used as a base image."

RUN \
	# Print executed commands
	set -x \
    # Update repository indexes
    && apk update \
    # Download the install script and run it
    && apk add curl \
    && curl -s -o /tmp/install-base.sh https://raw.githubusercontent.com/craftdock/Install-Scripts/master/alpine-base/install-base.sh \
    && sh /tmp/install-base.sh \
	# Clear apk's cache
	&& apk-cleanup


# Entrypoint
ENTRYPOINT ["/entrypoint"]
