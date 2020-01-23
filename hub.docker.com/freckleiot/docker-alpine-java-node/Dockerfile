FROM frolvlad/alpine-oraclejdk8:8.181.13-slim

MAINTAINER FreckleIOT

ENV LANG C.UTF-8

# install curl, bash and kms-env 0.3.0
RUN apk upgrade --update && \
    apk add groff less python py-pip curl bash nodejs npm && \
	pip install awscli && \
	apk --purge -v del py-pip && \
	rm /var/cache/apk/* && \
    npm install -g kms-env@0.3.0 s3-copy@0.0.2


COPY env-decrypt s3-cp /usr/local/bin/
ENTRYPOINT ["/usr/local/bin/env-decrypt"]
