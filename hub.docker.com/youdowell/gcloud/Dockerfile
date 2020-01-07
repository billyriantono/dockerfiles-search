FROM python:2.7.14-alpine3.6
MAINTAINER Andrew Usov <andrew.usov@youdowell.com>

RUN apk add --no-cache curl bash

WORKDIR /opt

# Install gcloud and kubectl
ENV GCLOUD_SDK_VERSION="176.0.0" \
	GCLOUD_SDK_SHASUM="34e65112c38e501435229029ed9f26017801de123b54c0416df6a4b5e1711a9b" \
	HOME="/opt" \
	PATH="/opt/google-cloud-sdk/bin:$PATH" \
	CLOUDSDK_PYTHON_SITEPACKAGES="1"

ENV 	GCLOUD_SDK_URL="https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${GCLOUD_SDK_VERSION}-linux-x86_64.tar.gz" \
	GCLOUD_SDK_FILENAME="google-cloud-sdk-${GCLOUD_SDK_VERSION}.tar.gz"

ADD ${GCLOUD_SDK_URL} ${GCLOUD_SDK_FILENAME}

RUN \
	(echo "${GCLOUD_SDK_SHASUM}  ${GCLOUD_SDK_FILENAME}" | sha256sum -c -) && \
	tar xf "${GCLOUD_SDK_FILENAME}" && \
	rm ${GCLOUD_SDK_FILENAME}

ENTRYPOINT ["/bin/bash", "-c"]
