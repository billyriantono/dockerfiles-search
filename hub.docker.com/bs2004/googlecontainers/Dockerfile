FROM alpine:latest

RUN set -xe \
	# Install required packages for build time. Will be removed when build finishes.
	&& apk add --no-cache --virtual .build-deps gnupg curl \
    && curl -SL "https://github.com/kubernetes/minikube/releases/download/v0.24.1/localkube" -o localkube