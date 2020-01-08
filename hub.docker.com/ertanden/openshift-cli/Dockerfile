FROM alpine:3.7
LABEL maintainer="Ertan Deniz <ertanden@gmail.com>"

WORKDIR /opt/oc

RUN apk add --update --no-cache \
        ca-certificates \
        curl \
        libc6-compat \
  && rm -rf /var/cache/apk/*

# specify the version string of the oc release
ENV OC_VERSION "v3.9.0"
ENV OC_VERSION_SHA "191fece"

# install the oc client tools
RUN curl -L https://github.com/openshift/origin/releases/download/${OC_VERSION}/openshift-origin-client-tools-${OC_VERSION}-${OC_VERSION_SHA}-linux-64bit.tar.gz > release.tar.gz \
    && tar --strip-components=1 -xzvf release.tar.gz \
    && mv oc /usr/bin \
    && rm -rf release.tar.gz
