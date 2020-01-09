#dockerhub images alluxio/alluxio:2.0.0
FROM alluxio/alluxio:2.0.0

LABEL maintainer="<rjhan@alauda.io>"

RUN apk del openjdk8 \
&& apk update \
&& apk upgrade \
&& apk add openjdk8 \
&& rm -vrf /var/cache/apk/*
