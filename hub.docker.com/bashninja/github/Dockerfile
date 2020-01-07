FROM lsiobase/alpine:latest

# set version label
ARG BUILD_DATE
ARG VERSION
LABEL build_version="Linuxserver.io version:- ${VERSION} Build-date:- ${BUILD_DATE}"
LABEL maintainer="Mike Weaver"

# environment settings
#ENV S6_BEHAVIOUR_IF_STAGE2_FAILS=2
ENV EDITOR="nano"
ARG USERNAME="username"
ARG EMAIL="username@users.noreply.github.com"

RUN \
 echo "**** install build packages ****" && \
 apk add --no-cache \
	git && \
 rm -rf \
	/root/.cache

COPY start.sh /

WORKDIR /git
ENTRYPOINT ["/start.sh"]
